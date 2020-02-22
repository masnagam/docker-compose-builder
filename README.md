# Install docker-compose using multiarch Docker image

```shell
curl -fsSL https://raw.githubusercontent.com/masnagam/install-docker-compose/master/run | \
  sh -s -- 1.25.4 | sudo tar -x -C /usr/local/bin
```

## How to invoke the build job

Manual trigger:

```shell
REPO=masnagam/docker-compose-builder
GITHUB_TOKEN='token...'
VERSION='1.25.4'

JSON=$(cat <<EOF
{
  "event_type": "build",
  "client_payload": {
    "version": "$VERSION",
    "latest": true
  }
}
EOF
)

echo "$JSON" | curl https://api.github.com/repos/$REPO/dispatches \
  -X POST -d @- \
  -H "Authorization: token $GITHUB_TOKEN" \
  -H "Content-Type: application/json"
```

## License

Licensed under either of

* Apache License, Version 2.0
  ([LICENSE-APACHE] or http://www.apache.org/licenses/LICENSE-2.0)
* MIT License
  ([LICENSE-MIT] or http://opensource.org/licenses/MIT)

at your option.

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in this project by you, as defined in the Apache-2.0 license,
shall be dual licensed as above, without any additional terms or conditions.

[LICENSE-APACHE]: ./LICENSE-APACHE
[LICENSE-MIT]: ./LICENSE-MIT
