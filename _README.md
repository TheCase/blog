```
# build
docker run -e DEBUG=true --rm -v ${PWD}:/srv/jekyll -it jekyll/jekyll:pages jekyll build

# broken on macos
# docker run --name blog.repulsor.net -e DEBUG=true --rm -v ${PWD}:/srv/jekyll -p 8080:4000 -it jekyll/jekyll:pages jekyll serve --watch --drafts

# view 
docker run -d -p 8080:80 -v ${PWD}/_site:/usr/share/nginx/html:ro nginx
sleep 3
open http://localhost:8080
```
