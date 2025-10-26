# cargo-ai-site

## overview

This repository contains the source code for the Cargo AI website.

## local development

To run the site locally:

```bash
zola serve
```

Then open [http://127.0.0.1:1111](http://127.0.0.1:1111) in your browser.

## building for deployment

To build the static site for deployment:

```bash
zola build
```

The output will be in the `public` directory.

## publishing to s3

Upload the contents of the `out` directory to your S3 bucket:

```bash
aws s3 sync out/ s3://cargo-ai.org --delete
```

## refreshing the cloudfront cache (via console)

After uploading new content to S3, you may need to clear cached files so your updates appear immediately.

To do this from the AWS Management Console:

1. Go to the **CloudFront** dashboard: [https://console.aws.amazon.com/cloudfront](https://console.aws.amazon.com/cloudfront)
2. Click your distribution ID associated with `cargo-ai.org`.
3. Select the **Invalidations** tab.
4. Click **Create Invalidation**.
5. In the **Object paths** field, enter:
   ```
   /*
   ```
   This tells CloudFront to refresh all cached files.
6. Click **Create Invalidation**.

After a few minutes, your new content will be visible globally.
