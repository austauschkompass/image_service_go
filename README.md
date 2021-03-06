# image_service_go

a work in progress


config.toml

```
[db]
dialect = "postgres"
name = "image_service"
username = "FOO"
charset = "utf-8"
host = "localhost"
password = "xxxxx"

[server]
name = "localhost"
port = 3010
debug = true
admin_token = "111111"
# array of CORS hosts
cors = ["http://localhost:3000"]


# storage can be either 's3' or 'local'
[storage]
type = "s3"

# expects credentials in env:
#	AWS_SECRET_ACESS_KEY
#	AWS_ACCESS_KEY_ID
[s3]
region = "eu-central-1"
bucket = "FOO"
host = "https://FOO.s3.eu-central-1.amazonaws.com"

[localstore]
assethost = "http://localhost:3010"
# below app path
directory = "uploads"
```


## Api

### GET Images


`curl --location --request GET 'http://localhost:3010/api/images'`

response:
```
[
  {
    "id": 48,
    "url": "http://localhost:3010/uploads/48-upload.jpeg",
    "filename": "48-upload.jpeg",
    "alt": "socialist fist",
    "copyright": "public",
    "category": "SuperCategory",
    "Variants": null
  },
  {...}
]
```

### GET Image 1

```
curl --location --request GET 'http://localhost:3010/api/images/1'

// response:
{
  "id": 1,
  "url": "http://localhost:3010/uploads/1-upload.jpeg",
  "filename": "1-upload.jpeg",
  "alt": "socialist fist",
  "copyright": "public",
  "category": "SuperCategory",
  "Variants": null
}
```

### Create Image Resource:

```
curl --location --request POST 'http://localhost:3010/api/images' \
--data-raw '{
    "alt":"socialist fist",
    "copyright":"public",
    "category":"politics",
    "data":"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"
}'

// response:
{
  "id": 50,
  "url": "http://localhost:3010/uploads/50-upload.jpeg",
  "filename": "50-upload.jpeg",
  "alt": "socialist fist",
  "copyright": "public",
  "category": "Politics",
  "Variants": null
}
```

### Update Image 1

```
curl --location --request PATCH 'http://localhost:3010/api/images/1' \
--data-raw '{
    "category":"My Category"
}'


// response:
{
  "id": 1,
  "url": "http://localhost:3010/uploads/1-upload.jpeg",
  "filename": "1-upload.jpeg",
  "alt": "socialist fist",
  "copyright": "public",
  "category": "My Category",
  "Variants": null
}
```

### Delete Image 42

```
curl --location --request DELETE 'http://localhost:3010/api/images/42'

```

## Variants

create/read/destroy variants, variants of given image


GET /api/variants

```
curl --location --request GET 'http://localhost:3010/api/variants'

// response

[
  {
    "id": 10,
    "width": 200,
    "height": 200,
    "filetype": "png",
    "url": "https://foo.s3.eu-central-1.amazonaws.com/60-10.png",
    "filename": "60-10.png",
    "name": "niceformatname",
    "ImageID": 60,
    "Image": {
      "id": 0,
      "url": "",
      "filename": "",
      "alt": "",
      "copyright": "",
      "category": "",
      "Variants": null
    }
  },
  {...}
]
```

GET /api/images/42/variants

```
curl --location --request GET 'http://localhost:3010/api/images/42/variants'

// response

[
  {
    "id": 10,
    "width": 200,
    "height": 200,
    "filetype": "png",
    "url": "https://foo.s3.eu-central-1.amazonaws.com/60-10.png",
    "filename": "60-10.png",
    "name": "niceformatname",
    "ImageID": 42,
    "Image": {
      "id": 0,
      "url": "",
      "filename": "",
      "alt": "",
      "copyright": "",
      "category": "",
      "Variants": null
    }
  }
]
```

POST /api/images/42/variants

```
curl --location --request POST 'http://localhost:3010/api/images/60/variants' \
--data-raw '{
    "width":200,
    "height":200,
    "filetype":"png",
    "keep_ratio": true,
    "name": "niceformatname"
}'


// response

{
  "id": 10,
  "width": 200,
  "height": 200,
  "filetype": "png",
  "url": "https://foo.s3.eu-central-1.amazonaws.com/60-10.png",
  "filename": "60-10.png",
  "name": "niceformatname",
  "ImageID": 60,
  "Image": {
    "id": 0,
    "url": "",
    "filename": "",
    "alt": "",
    "copyright": "",
    "category": "",
    "Variants": null
  }
}
```

DELETE /api/variants/1

```
curl --location --request DELETE 'http://localhost:3010/api/variants/1'
```
