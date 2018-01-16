# Farmers Fire - Junior Developer - Sample Application
Thanks for your interest in our Jr Dev position!  If you've been asked to complete this project, that means your resume looked good, you've been given further details on this job, and now we'd like to see your existing skills (along with your ability to learn and apply new technologies) put to the test.

## The business need
A relatively small P&C Insurance Carrier will still have 10,000+ annually-renewing insurance policies of different policy types (Homeowners, Dwelling, Commercial, etc).  During the lifecycle of a policy, certain events may require a formal letter to be generated and sent to the insured, agent, mortgagee, etc.  Many of these letters have common content/structure that can be reused time and again for different policies (eg standard header/footer including company wordmark, policy number and type, date generated; mailing address block pre-filled with the policyholders address; opening and closing paragraphs, etc).  Your task will be to create a sample application that allows a user to:

1. Search for the policy they need to send a letter on, by insured name, policy number, policy type, etc
2. Select the desired policy from the matched results
3. Choose from a set of pre-defined Letter templates which letter they want to generate
4. Generate the letter, with the selected policy/policyholder details being dynamically rendered in place

## Your tech stack
To get you started with technologies we use at Farmers Fire, we will prescribe most of what you should use for this project.  Should you ultimately not be selected for this position, exposure to these frameworks and technologies should have value for many similar developer positions:

### Hosting
* You are welcome to host this sample application however is most cost-effective (free) for you.  If you already have hosting established for other projects, feel free to use that.
* If you don't have hosting established or do not want to put this sample project on there, we recommend starting with an [AWS Free Tier](https://aws.amazon.com/free/) EC2 instance, preferably running Ubuntu 16.04.
* **_Extra credit:_** bypass traditional hosting altogether and package your application using [Zappa](https://www.zappa.io/) for Serverless deployment on AWS Lambda / API Gateway.

### Server-side
* On the server you'll be using [Python](https://www.python.org/) - your choice between version 2.7 or 3.6.
* Use [pip](https://pip.pypa.io/en/stable/quickstart/) to install and manage your packages and their depedencies.
* Be sure to create a [VirtualEnv](https://virtualenv.pypa.io/en/stable/) to isolate and simplify installation of your library dependencies ([VirtualEnvWrapper](https://virtualenvwrapper.readthedocs.io/en/latest/) is a great convenience-script for handling your venvs).
* Use [Flask](http://flask.pocoo.org/) for your WSGI application framework.
* Since you're using Flask, you'll want to use [Jinja2](http://jinja.pocoo.org/docs/2.10/) for your templates (be sure to utilize [template inheritance](http://jinja.pocoo.org/docs/2.10/templates/#template-inheritance) between a base layout template and your individual pages/sections).

### Database
* MySQL, SQLite, PostgreSQL - your choice.
* Use [SQLAlchemy](http://docs.sqlalchemy.org/en/latest/) for your ORM.
* Since you're also using Flask, use [Flask-SQLAlchemy](http://flask-sqlalchemy.pocoo.org/2.3/) to speed up and standardize your usage.  
* To simplify the creation and maintenance of sample data, you may want to use [Flask-Admin](http://flask-admin.readthedocs.io/en/latest/) for front-end CRUD workflows (you do not have to worry about authentication/authorization for this sample app, but you can add if you like).

### Client-side
* As this isn't a designer position, looks are not the focus of this app (but if you are able and want to flex on looks after functionality is completed, that would be good **_extra credit_**).
* Make it easy on yourself and use a frontend css framework like [Bootstrap](https://getbootstrap.com/) or [Foundation](https://foundation.zurb.com/).
* For your policy search and results interactions, you may use traditional `<form>` element's native `submit` functionality to POST your http request to the server and return a rendered template response with a page reload;
    * however, for **_extra credit_**, use [knockout.js](http://knockoutjs.com/) or [vue.js](https://vuejs.org/v2/guide/) for MVVM-driven UI and dynamically post your search params and load results into a results table without a page-reload, for instance, using [axios](https://github.com/axios/axios) (or [jQuery](https://jquery.com/) and patching in a [convenience postJSON method](https://gist.github.com/alexgann/c59b3330ba4402840b7dc692c1ea8a7e)).
* Please take advantage of a CDN like [cdnjs](https://cdnjs.com/) for all of your standard js and css libraries.

### Source control
* You should start a new public GitHub repo for this project and clone it down to your development instance.
* As you work and complete incremental pieces of functionality, commit your changes (eg `git commit -am "base jinja template completed"`) and ultimately push those commits back to your repo.
* Strike a natural balance between having a single monolithic commit after completing your entire project, and having hundreds of micro-commits for each line of code you've changed.  A good rule of thumb is to commit whenever you've functionally completed a specific aspect of your application.
* The submission of your project should include both a link to the running application (plus any credentials to the front-end admin if you decide to implement that) and a link to your GitHub repo for code review.

### Data model
* Your application should utilize at least two SQLAlchemy entity models: `Policy` and `Contact`.
* For simplicity, the relationship between these entities can be a simple many-to-one Policy-to-Contact (ie, each policy is assigned to just one contact (through a contact_id foreignkey column) and a single contact can thereby have multiple policies).
    * Beyond your relationship back to a single `Contact`, your `Policy` model might have some String fields like `policy_number` or `policy_type` (`PolicyType` would really be its own model as well, but again, simplifying here), and perhaps a Date `effective_date` column and some standard `created` and `updated` datetime columns.
    * Your `Contact` model should then have some String fields like `first_name`, `last_name`, and some address fields for a mailing address block.
    * **_Extra credit_** - instead of hard-coding your various (2 is sufficient) Letter templates that the user selects from, you could make `Letter` itself an entity model in the database, with String `name` and `description` fields, along with a Text field for the jinja template itself for the letter.  Each letter could still `extends` a base letter template, but then you could use Flask-Admin to create and maintain your Letter templates, and use Flask's [render_template_string](http://flask.pocoo.org/docs/0.12/api/#flask.render_template_string) to render it.

### Other considerations
A few more potential ideas for **_extra credit_** (these are just suggestions, feel free to flex however you like):
* It is sufficient for the selected Policy + Letter to render as html to a new tab; however, you might provide the option to render the letter directly to a pdf using, for instance, a [wkhtmltopdf wrapper like pdfkit](https://github.com/JazzCore/python-pdfkit).
* Sometimes, in addition to the pre-defined letter language, the user may need to inject some language in the middle, or modify some of the standard language.  Add an editor/live-preview of the letter after the Policy/Letter type have been selected, perhaps using [trix](https://trix-editor.org/).
* The user may at times need to batch-generate the same standard letter for multiple policies.  Extend the search results to allow for multi-selection and batch generation of the rendered letters.
* Some search interfaces will list each individual field you can search on (eg First Name, Last Name, Policy Number, Policy Type) etc.  This can be useful in an "Advanced Search" interface, but consider presenting a single search field that can intelligently/efficiently search against multiple fields.
* We are hoping to make our hiring decision **before month-end February, 2018** so you safely have until around **Friday, 2/23** to complete as much as you are able.  To submit your project or request clarification, simply reply back to the SmartRecruiters message where you were invited to start this project.

### GLHF
The Farmers Fire Insurance Company
