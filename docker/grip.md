# Grip

Run a markdown previewer using the Github markdown styles for your README.md:

```bash
docker run -it --name python-grip --rm \
    -p 6419:6419 \
    --env FILE=README.md \
    --env DEBUG=True \
    --env DEBUG_GRIP=True \
    --env HOST=0.0.0.0 \
    -v "$(pwd)":/workspace \
    python bash -c "pip install grip && mkdir ~/.grip/ && bash -c \"echo -e \\\"DEBUG=\$DEBUG\nDEBUG_GRIP=\$DEBUG_GRIP\nHOST='\$HOST'\\\" >> ~/.grip/settings.py \" && cd workspace/ && grip \$FILE"
```

[Source](https://github.com/joeyespo/grip/issues/356)
