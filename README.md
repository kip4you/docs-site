**Adding Pubs**
Modify the file \_data/publications.yml to add a new entry. Make sure to follow the docs format.

**Running locally with docker**

```bash
docker run --rm --volume="$PWD:/srv/jekyll" -p 4000:4000:4.2.0 -it jekyll/jekyll jekyll server
```
