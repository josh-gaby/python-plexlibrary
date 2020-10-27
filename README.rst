Python-PlexLibrary
==================

Python command line utility for creating and maintaining dynamic Plex
libraries and playlists based on "recipes".

E.g. Create a library or playlist consisting of all movies or tv shows in a Trakt_ list or
on an IMDb_ chart that exist in your main library, and set the sort titles
accordingly (sort only available for libraries).

.. _Trakt: https://trakt.tv/
.. _IMDb: https://imdb.com/

Known limitations / Warning
---------------------------
**\*\*Supports new Plex Movie Agent\*\***

For the Plex Movie Agent to work, you must be using Plex Media Server 1.20.1.3213 or newer and the metadata for the library **MUST** have been refreshed using PMS >= 1.20.1.3213

This fork will run best if it is on the same system that the Plex Server is on due to the direct db access requirement. It can be run on a remote server but each time it is run a copy of the database will be downloaded from the Plex server which might be a lot of data transfer for bigger libraries.


Disclaimer
----------
This is still a work in progress, so major changes may occur in new versions.

Requirements
------------
* Plex media server version 1.20.1.3213 or newer

* Python 3

* You need a trakt.tv account and an API app: https://trakt.tv/oauth/applications/new

* (optional) The Movie Database API

  * https://developers.themoviedb.org/3/getting-started
    
  * Required for fetching scores, release dates etcetera, for weighted sorting 
    
  * Required for matching any library items that use the TMDb agent with the items from the lists (if those items do not include a TMDb ID)
    
  * Shouldn't be necessary for Trakt, as those usually all have TMDb IDs.

  * Required for matching movies and some TV shows sourced from IMDb

* (optional) TheTVDB API

  * https://www.thetvdb.com/?tab=apiregister
    
  * Required for matching any library items that use the TheTVDB agent with the items from the lists (if those items do not include a TheTVDB ID)
    
  * Shouldn't be necessary for Trakt, as those usually all have TVDB IDs.

  * Required for matching TV shows sourced from IMDb

Getting started
---------------

1. Clone or download this repo.

   .. code-block:: shell
   
      git clone https://github.com/josh-gaby/python-plexlibrary.git
      
2. Switch to this branch.
   
   .. code-block:: shell
   
      git checkout direct-db-access

3. Install Python and pip if you haven't already.

4. Install the requirements:

   .. code-block:: shell

       python3 -m pip install -r requirements.txt

4. Copy config-template.yml to config.yml and edit it with your information.

  * Here's a guide if you're unfamiliar with YAML syntax. **Most notably you need to use spaces instead of tabs!** http://docs.ansible.com/ansible/latest/YAMLSyntax.html

5. Check out the recipe examples under recipes/examples. Copy an example to recipes/ and edit it with the appropriate information.

Updating
--------
You can make sure you have the latest changes by changing to the directory you cloned this repo to and doing a git pull followed by a requirements install to make sure all requirements are up to date:

.. code-block:: shell

    git pull
    python3 -m pip install -r requirements.txt
    

Usage
-----
In the base directory, run:

.. code-block:: shell

    python3 plexlibrary -h

for details on how to use the utility.

.. code-block:: shell

    python3 plexlibrary -l

lists available recipes.

To run a recipe named "movies_trending", run:

.. code-block:: shell

    python3 plexlibrary movies_trending
    
**(If you're on Windows, you might have to run as admin)**

When you're happy with the results, automate the recipe in cron_ or equivalent (automated tasks in Windows https://technet.microsoft.com/en-us/library/cc748993(v=ws.11).aspx).

.. _cron: https://code.tutsplus.com/tutorials/scheduling-tasks-with-cron-jobs--net-8800

**Pro tip!** Edit the new library and uncheck *"Include in dashboard"*. Othewise if you start watching something that exists in multiple libraries, all items will show up on the On Deck. This makes it so that only the item in your main library shows up.

Planned features
----------------
See issues.

Credit
------
Original functionality is based on https://gist.github.com/JonnyWong16/b1aa2c0f604ed92b9b3afaa6db18e5fd

