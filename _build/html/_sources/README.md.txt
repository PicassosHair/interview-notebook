# Interview Notebook

## Welcome
I start to compile notes for preparing interviews. In the algorithm part, I try to aggregate similar problems and summary the common solutions. I believe it is helpful. If you find anything wrong or you want to share your own ideas, feel free to make a PR.

[Interview Notebook](https://picassoshair.github.io/interview-notebook/_build/html)

## Sphinx Setup 
I use Ubuntu Docker Container for setting up Sphinx and building the static webpages.

```bash
apt-get update

# Install Sphinx
apt-get install python3-sphinx

# Install pip
apt-get install python3-pip

# Install recommonmark for md file supporting 
/bin/pip3 install recommonmark

# Install sphinx-rtd-theme
/bin/pip3 install sphinx-rtd-theme

# Build static webpage
make html
```

## Github Pages 
The `main` branch is for notes. The `gp_pages` branch if for holding the static website.

