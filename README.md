# Distributed Knowledge Graphs


## Project Structure

```bash
bin #A folder to put your scripts (.bat for Windows or .sh for macOS and Linux)
images #A folder where to put the screenshots that you generate.
Task 3 #A node project to implement a HTTP server for Task 3
└── app.js # The server code (TODO: complete)
└── index.html #The Web page
└── package.json #A JSON used by Node.
Report.md #The Report to complete
README.md #This README.
```



## Task 1: Creating a profile on Solid (2pt)

Go to https://solid.interactions.ics.unisg.ch/idp/register/ and create a Solid Pod for each group member.

WARNING: If you edit your WebID profile with a file that is not a proper Turtle document, you will lose access to your Pod. You can use a Turtle editor (e.g., https://ci.mines-stetienne.fr/teaching/semweb/turtle.html) to edit your profile and ensure that it satisfies the right Turtle syntax. Also, you MUST NOT remove any information created at the creation of the pod as this information is required for connecting an app to the Solid pod.

Use a Pod editor, such as Penny (https://penny.vincenttunru.com) to edit your Pod. Your Pod provider is https://solid.interactions.ics.unisg.ch/.

One group member creates in his/her Pod a Turtle page to represent the group and indicates the group members using the FOAF ontology.

To make the created profile, and any further created documents, readable by anyone do so, use the Penny application to create the Access Control List for the created Turtle document and set the read permission for everyone in this control list. You also need to set the write permission to be able to make further changes to your document.

Example of such a group: https://solid.interactions.ics.unisg.ch/jlemee/bcs-ds-2024-ta-group

The group members updates their WebId profiles to indicate their name, mail box, and group they belong to.

Example of such a profile: https://solid.interactions.ics.unisg.ch/jlemee/profile/card#me

These different pages should be linked in the Report.

Use a Linked Data browser, such as these Chrome: https://chromewebstore.google.com/detail/openlink-structured-data/egdaiaihbdoiibopledjahjaihbmjhdj or Firefox: https://addons.mozilla.org/en-GB/firefox/addon/rdf-browser/ plugins, to navigate the distributed social graph.



## Task 2: Query the distributed social graph (2pt)

First, if you do not have npm, you have to install it. Information on how to this are available here: https://nodejs.org/en/download/package-manager

Install Comunica with:

```bash
npm install -g @comunica/query-sparql
```

1. Perform a comunica-sparql query to get your group from your WebId.

Install Comunica for Link Traversal with:

```bash
npm install -g @comunica/query-sparql-link-traversal
```

2. Perform a comunica-sparql-link-traversal query to get your social graph (friends and friends of friends recursively) from your WebId. Compare with the result of the request performed without link traversal.

You can use the syntax subject (predicate)+ object in your SPARQL query to follow the links providedin the subject or resource.


# Task 3: A Solid-Based Application (1pt)

Use the application MediaKraken (https://noeldemartin.github.io/media-kraken/) to add movies to the Solid Pod of at least one member of your group. After that, the movies are included as files in the \texttt{movies} container in the pod but the \texttt{movies} folder is not public. To do so, use the Penny application to create the Access Control List for the created \texttt{movies} container and set the read permission for everyone in this control list. Look at https://solid.interactions.ics.unisg.ch/jlemee/movies/ for an example of such a created container

You should then complete the provided JavaScript project template [`app.js`](Task%203/app.js), and potentially [`index.html`](Task%203/index.html), for creating a Node Web application, using the Comunica framework (https://comunica.dev/docs/query/getting_started/query_app/), that retrieves the names of all movies stored in your Pod by MediaKraken.

You should use the QueryEngine called engine to perform Comunica requests. You should reinstantiate it for each SPARQL request you make. You can perform a new query within the then method of a given query. If you need to use link traversal, use the QueryEngine from the @comunica/query-sparql-link-traversal npm package.

You can use the command ```bash npm i ``` to load the node modules from the Task 3 folder.

You can then use the command ```bash npm start ``` to start the application. Then, go to http://localhost:5000 to see the Web page.


WARNING:  If you encounter an issue when connecting to MediaKraken, please follow these steps:
1) Ensure that the movies/ container is not present in your Pod or delete it if it is. This is because the container will be created by MediaKraken.
2) Create a settings/ container in your Pod if one is not already present.
3) In this container, add an empty file named privateTypeIndex and keep it empty.
4) Ensure that in your WebID profile, a link to the privateTypeIndex is present of the form:<#me> solid:privateTypeIndex <https://solid.interactions.ics.unisg.ch/jlemee/settings/privateTypeIndex> .
As an example for the last step, you can have a look at my profile: https://solid.interactions.ics.unisg.ch/jlemee/profile/card#me. 


