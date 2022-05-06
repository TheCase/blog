docker run -e DEBUG=true --rm -v ${PWD}:/srv/jekyll -it jekyll/jekyll:pages jekyll build

docker run --name blog.repulsor.net -e DEBUG=true --rm -v ${PWD}:/srv/jekyll -p 8080:4000 -it jekyll/jekyll:pages jekyll serve --watch --drafts
