# S3 Filed


```ts
import { S3Config, s3File, s3Image } from '@k6-contrib/fields-s3';
import 'dotenv/config';

const s3Config: S3Config = {
  bucket: process.env.S3_BUCKET, // name of bucket
  folder: process.env.S3_PATH,
  baseUrl: process.env.S3_BASE_URL, // if provided the url is not compouted from endpoint and folder, rather use this as `${baseUrl}/${filename}`
  s3Options: {
    accessKeyId: process.env.S3_ACCESS_KEY_ID,
    secretAccessKey: process.env.S3_SECRET_ACCESS_KEY,
    endpoint: process.env.S3_ENDPOINT, // use region for aws, endpoint for s3 compatible storage
  },
  uploadParams() {
    return {
      ACL: 'public-read', // needed to make it public
    };
  },
};

const Post = list({
    fields: {
      title: text({ isRequired: true }),
      content: text(),
      image: s3Image({ s3Config }),
      file: s3File({ s3Config }),
    },
  }),
```