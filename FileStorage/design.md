> Functional Req

- upload files
- download files
- list files and folders
- file/folder operations (create, delete, move, rename)
- share files with others
- support large file uploads and resumable uploads
- maintain file versions

> Non-functional

- Scalability (handle millions of users and files)
- Availability (upload/download should be highly available)
- Durability (prevent data loss)
- Performance (low latency to view files)
- Consistency (metadata and file permissions should be consistent)
- Security (Authentication, Authorization and encription)

> Estimation calculation

- total users 10M
- daily active users 1M
- daily uploads 5M
- Avg file size 5mb
- daily storage growth 25TB
- Annual storage growth ~9.1PB

daily storage:
no of uploads/sec
peak traffic 5x avg

> API

- POST - /files/upload/initiate
- PUT - /files/upload/:uploadId/parts/:partId
- POST - /files/upload/:uploadId/complete
- GET - /files/:fileId/download
- POST - /files/:fileId/share
- GET - /files/:fileId/versions

> Data Modeling

- Users (id, name, email, storage_capacity, storage_used)
- Files (id, name, type, current_version, creator_id, status)
- Folder (id, name, size, creator_id)
- Node (id, parentId, resource_type: FILE | FOLDER, resource_id, creator_id)

- Uploads (id, file_id, storage_upload_id, content_type, file_size, chuck_size, total_parts, status, expires_at, created_at)
- Upload_parts (id, upload_id, part_number, eTag, checksum, status)

- File_versions (id, file_id, version_number, size, checksum, content_type, storage_key, status)
- File_permissions (id, resource_id, resource_type, user_id, permission: VIEW | EDIT)

Soft Deletion: status (ACTIVE | TRASHED | DELETED)
Uploads status: INITIATED | UPLOADING | COMPLETED | FAILED

> High level architecture

> Deep dive

- File Mulitpart upload
- File download
- File sharing
- File versioning

> Bottleneck & failures

- Large file uploads - Multipart uploads
- Network interruption - Resumable uploads
- Backend Overload - Direct Object storage transfers
- Metadata database overload - replicas, indexing, sharding
- Frequent metadata reads - in memory cache
- Object uploaded but DB update fails - Reconcilation worker
- Duplicate upload completion - Idempotency
- Unauthorized downloads - short lived urls
- Storage failures - Replication and backups
