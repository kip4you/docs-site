**Adding Docs**

- Add markdown file under under **_pages** folder
- Add images under **_assets/images**
- Modify **_data/navigation.yml** under **docs:** to add a reference to the new file permalink

**Running locally with docker**

```bash
docker run --rm --volume="$PWD:/srv/jekyll" -p 4000:4000 -it jekyll/jekyll:4.2.0 jekyll server
```
