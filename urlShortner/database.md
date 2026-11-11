```sql
CREATE TABle shortend_urls (
    id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    orginal_url TEXT NOT NULL,
    created_at TIMESTAMP NOT NULL,
);

INSERT INTO shortend_urls(original_url)
VALUES (""), ("");

SELECT original_url
FROM shortend_urls
WHERE id = <decodedBase64Id>;
```

```redis
SET KEY VALUE

SET KEY VALUE EX 3600

TTL KEY

GET KEY - retuns value or (nil)

DEL KEY

EXISTS KEY
```
