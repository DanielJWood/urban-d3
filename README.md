## About

This is a codebase that will allow energy.gov users to quickly get started developing new graphics and maps. By cloning this repo, you can immediately begin coding. 

The contents of this page are in the Public Domain

## Dependencies
- Git (_[tutorial](https://try.github.io/)_)	
- Download and install [Jekyll](http://jekyllrb.com/). [Jekyll Documentation](https://jekyllrb.com/docs/home/) and specific documentation about [Jekyll and Github Pages](https://jekyllrb.com/docs/github-pages/).
- [Pym.js](http://blog.apps.npr.org/pym.js/) is used for making fully responsive iframes. 
- [Foundation CSS](http://foundation.zurb.com/sites.html) is often used but not required. 
- Note: If it's your first time running this stuff, you may need admin access.

## Setup

- Before Getting started, create a new repo in the [EnergyApps Github group](https://github.com/energyapps) or elsewhere.

- Ensure that Jekyll is installed on your computer. (And read up on the directory structure on their site and below). 

- In your local git projects directory clone the app_frame repo:

`git clone https://github.com/energyapps/app_frame.git`

- Rename the folder to your project name

`mv app_frame/ new_directory_name/`

- cd into that folder in terminal and change remote URL to new repo:

`git remote set-url origin https://github.com/energyapps/NEW-REPO-NAME.git` -changes the remote url to your new URL

- Push to this new repo

`git push -u origin master`

- Branch out the gh-pages branch

```
git branch gh-pages
git checkout gh-pages
git push origin gh-pages
```

- At this point you may want to go into your repo on github and change the "default branch" to gh-pages in the settings. The gh-pages repo is like the "production server". Whatever is in this repo is what is served over `https://energyapps.github.io/NEW-REPO-NAME`.

## Building your graphic

- Build the Jekyll `_site/` folder by running `jekyll build` in your directory. I recommend running `jekyll build --watch`, which automatically rebuilds your `_site` folder whenever you change something in the repository. More on this [on jekyll's website](https://jekyllrb.com/docs/usage/).
- Run the jekyll server by running `jekyll serve`. You can now see your page at http://localhost:4000/
- Begin work in the `index.html` file, `style.css` file, and `script.js` file. Edit libraries in `_layout/default.html`.
- Push changes to github, see website running remotely at `https://energyapps.github.io/NEW-REPO-NAME/`. The site is now deployed on energyapps.github.io
- Recommended: Update README.md to reflect your current project.

## Deploying your graphic on energy.gov

- Log into the cms. Click on `Add Content` and then `Map` and select a group. 
- Add Title.
- Make sure "Hide Map Title" and "CSS Scaling" are **NOT** clicked.
- Ignore "Map Library" field. This is an artifact. 
- Make sure that the "Map Type" is set to "Raw Embed"
- Following the directions/explanations laid out below in the Contents section, paste in the contents of _pym_files/ files. 
	- Ensure that a fallback image has been added to "markup.html"
	- Ensure that you have updated the URL on "cms.js"
- **Important** add a thumbnail image to the CMS.
- Add any remaining tags and fields you may want. 
- Click Save and see the graphic on resulting page. 
- After recieving the green light, publish this page. 
- Find the map name in an article you are building and select it with the "map reference" option.

## Contents

To get an in-depth look at the directory structure of a general [jekyll site go here](https://jekyllrb.com/docs/structure/).

1. 	root directory
	* README.md 
		- You are here.
	* index.html 
		- Contains the markup that you are creating. Will be merged into _layouts/default.html
	* _config.yml
		- Contains meta data for jekyll. Read more detailed info [here](https://jekyllrb.com/docs/configuration/).
	* .gitignore 
		- Contains any files, folders, or file types that you may want git to ignore when it is looking for files to add, commit, and push. By default, we exclude some mac files, and the _site/ folder.
2.	_layout/
	* The _layouts/ folder is the Jekyll folder that contains layouts for any type of page within a jekyll site. 
	* default.html
		- This is a very rough cannibalization of the DOM elements in energy.gov/maps element. NOTE, this has not yet been updated from the previous energy.gov design.
		- All CSS and JS should be linked here. Any library you want to link should be added or removed from here. Mapbox is the default.
		- Pym is linked here by default.
		- Jekyll merges in the markup from the index.html file here. 
3.	_site/
	* This is the folder that is generated by Jekyll and holds the merged static webpages. You do not need to add or subtract anything from it, as it should automatically update. Additionally, it is not pushed to github, as github builds this folder automatically when `_config.yml` is present.
4. js/
	* script.js
		- script that executes all commands on graphic. Included at the top of this file is the initiation of pym for the child page. 
	* various scripts and libraries you may need. 
5. css/
	* style.css
		- custom css to be added to map. CSS that would be added to the maps content type.
	* master_style.css
		- A static copy of the above as a fallback when the energy.gov links break. NOTE: This is a copy of the old master CSS of energy.gov prior to its 2017 redesign. Does not yet reflect the change of design. 
	* fonts.css
		- a collection of some commonly used energy.gov fonts. NOTE: Avenir has been replaced by Karla as its font. Therefore fonts.css does not yet reflect this change. 
6.	pym_files/
	* **This folder contains the files that you will add to the maps section of the CMS**
	* Refer to [pym's documentation](blog.apps.npr.org/pym.js/) to fully understand how it works.
	* markup.html
		- This file contains the html that you will paste into the CMS "markup" section. 
		- Contains the html that will allow for fallback image to display when the graphic is reached from Internet Explorer. In order to make sure this works, add a fallback image to the CMS and put its link in the "<img>" there. 
		- The div with id of "graphic" is where pym operates on. 
	* cms.js 
		- Javascript required to make pym work. Contains pym library and the pym initiator. 
		- **IMPORTANT**: Remember to edit the following line to contain the URL to this project's github pages URL. `var pymParent = new pym.Parent('graphic', 'https://energyapps.github.io/NEW-REPO-NAME/', {});`
		- Make sure that this URL is serving over HTTPS. 
		- After you've updated the file, copy the contents and paste them into the CMS under the "custom JS" section. 
	* cms.css
		- CSS required to make fallback work as planned, pasted into CMS under the "custom CSS" section
	* child.html
		- For reference, contains the minimal html/js needed on the child page in order for the above parent page to work. This is embedded within "default.html" and "script.js" so there is no need to add it anywhere.
	* pym.min.js is a copy of the pym library.
	
## Notes

- used to use Foundation CSS a lot, so you may want to understand how that works. 
- needs, update the styles to be current with the new css. 
- Crowbar for D3
- http://meethyde.com/ could be useful in the future for something. 