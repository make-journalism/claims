# Claims
Form builder for a claims-based reporting tool.

## Machine Terms / Intent
This is a temporary/disposable machine that accepts structured data inputs from trusted reporters in order to gather and collaborate on important data about the world.

## Interface (WIP)
As this is supposed to be used to spin-up short-lived instances of data entry portals, the interface will be a simple command-line tool that will make use of several pre-determined inputs. The [Yeoman](https://yeoman.io) tool will be used to generate this interface and the resulting machine.

As in a scripted environment:
`$ claims --field-list=fields.csv --claim-list=claims.csv --reporters=npr.org --server=<server auth> --data=<data auth>`

Using prompts:
`$ claims`

We also intend for this to be available on NPM once complete, so you could use their `npx` tool to run it whether you have a local copy or not:
`$ npx make-journalism/claims`

### Options
* `field-list` is intended to be exactly as named.
	- Columns should be: `name`, `type`, `description`, `limit`, `required`
	- `type` should be one of: `email`, `claim`, `text`, `textarea`, `select`
	- `limit` will be the character length limit for a text or textarea, a selection limit (if you want to make a field multiple select), or the number of submissions which can be entered under each claim type (if not included, default limit is one report per claim)
	- `options` is only a valid type for `select` types, and should be left empty for the other field types
	- `required` can be any non-empty value; if no value is provided for this column, the field will not be required
	- You must provide `email` and `claim` field types, as needed for the authentication and to match with the claim list
	- `email` and `claim` fields must also be marked `required`, and only one of each of these types will be allowed
* `claim-list` should be a simple list of string values, which will be used in the above-mentioned `claim` field type, as a selection or auto-complete source
* `reporters` can be one of the following
	- single valid domain name
	- comma separated list of domain names
	- Regular Expression to validate multiple domains
* `server` should be the name of a service, followed by the credentials for that service, e.g.: `aws:<key>:<secret>`
	- initially only AWS will be supported, though we hope to quickly provide access via Azure, Google Cloud, et. al.
* `data` should be the same as service -- the name of the data provider, followed by the credentials for access
	- initial support for Airtable, though as above we intend to quickly support other providers

## To-Do
As there is a great deal yet to do on this project, this will be broken into sections as makes sense.

### Interface
* Build the initial generator structure with the above-mentioned arguments set in place but running no-op functions or `this.log('arg placeholder')`
* Accept options from the command line once prompts are available, with a way to skip a prompt if the option is initially provided
* ???

### Option processing
* Generate the form from the field list
* Parse the claim list and register the resulting claim options with the form
* Register the reporters option with the form authenticator
* Set up the Serverless configuration with the provided server credentials
* Set up the cloud data storage with the provided data credentials

### Form building
* TBD

### Editorial Queue
* TBD
