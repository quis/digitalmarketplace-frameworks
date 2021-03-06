Digital Marketplace content
===========================
YAML definitions of the Digital Marketplace’s procurement frameworks.

Question keys
-------------

* `question` name of the question, displayed in forms and summary tables (required)
* `type` type of the question input, used to find the related toolkit form template (required)
* `hint` hint text to display after the question name
* `optional` if set to `true` makes the question optional
* `options` a list of possible values for the types that support them. Each option consists of:
    * `label` text displayed on the option label (required)
    * `value` value submitted to the server when the option is selected
    * `filter_label` [currently unused] text displayed in the buyer frontend filters list instead of label
    * `description` additional text displayed after the option label (used for `lot` question)
* `validations` a list of validation errors related to the field. Each validation conists of:
    * `name` the error message key that should match the validation error returned by the API (required)
    * `message` text of the message that will be displayed by the frontend app (required)
* `depends` describes the service conditions that must be met for question to be displayed. Right now, only used to list the
  lots the question applies to. Each depend rule consists of:
    * `"on"` service data key name to use for comparison (e.g. "lot" for lots)
    * `being` a list of acceptable values for the key. If service data key value matches one of the values in the `being` the
       question is kept, otherwise the question is removed from the section for the given service
* `list_item_name` [currently unused] text displayed in the "Add another ..." button and item names by the list-entry inputs
* `assuranceApproach` contains the name of the set of possible assurance answers for the question. Assurance answer sets are
  listed in the supplier frontend.
* `fields` a mapping of toolkit form field key to the service data key used for multi-input field types (e.g. pricing)
* `max_length_in_words` sets the limit on question value length in words

Running the tests
-----------------

The tests check that the YAML files are valid and that they match a schema.

Setup a VirtualEnv
`mkvirtualenv`

Install dependencies
`pip install -r requirements_for_test.txt`

Run the tests
`py.test`

Versioning
----------
Releases of this project follow [semantic versioning](http://semver.org/), ie
> Given a version number MAJOR.MINOR.PATCH, increment the:
>
> - MAJOR version when you make incompatible API changes,
> - MINOR version when you add functionality in a backwards-compatible manner, and
> - PATCH version when you make backwards-compatible bug fixes.

To make a new version:
- update `VERSION.txt` with the new version number
- commit this change; the first line of the commit message **must** be in the
  format `Bump version to X.X.X`
- create a pull request for the version bump

When the pull request is merged a Jenkins job will be run to tag the new
version.
