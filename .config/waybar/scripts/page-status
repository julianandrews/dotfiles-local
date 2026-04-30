#!/bin/sh

curl -sLI "$1" -w '%{http_code}' --max-time 5 | grep -q '^200$' \
    || echo '{"text": "down", "alt": "down"}'
