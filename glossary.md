# Glossary

* `Survey`: A solicitation for input from a `Respondent`. There are two types of
  surveys: Application surveys and Societal Benefit surveys.
* `Response`: A completed survey.
* `Library`: The collection of all `responses`.
* `Registry`: The collection of available `survey objects`. `Experts` can either select
  existing items or add to the registry when submitting a `response`.
* `Analysis`: The process of converting many survey responses to a Sankey diagram by an
  `Analyst` interacting with the `Library`. Surveys are searched by title and `tags`.


## Registry

A list of available `response objects`. Drives consistency in naming across `surveys` to
support `analysis` and also to ease data entry for `Experts`, over time.

Is suspect that we can just have a basic Registered Survey Object that has generic
fields whether it is a Data Product, Observing System, Etc. We probably need to have a
separate structure to register Societal Benefit Analysis framework.

_TODO_: Seek input from Bill Manley, ADC, Federated Search crew. Can we import or sync
items in the registry from an external source?

* `Name`
* `Type`: `Observing system`, `data product`, `application`, `SBA`
* _TODO_: Other fields?


## Surveys

* `Name`: Unique name of survey
* `Description`
* `Type`: Surveys could be requesting information about the current state or desired
  state of `response subjects`. For "desired state" surveys, we wouldn't be interested in
  `gaps`. (_TODO_: This concept needs to be refined in the future.)


### Responses

* `Respondents`: `Experts` who can contribute to `response`.
* `Tags`: Arbitrary strings for grouping surveys. For example: `river-watch`.
* `Version`: Surveys can be re-issued, with changes, as a new version. E.g. a new survey
  is created as version "1" (version may be represented to user as creation date).
  Later, the survey is copied to version "2", altered, and re-issued, possibly to a
  different `expert`. We also copy the old response to the new version so the
  `Expert(s)` do not need to start from scratch.
* `Validated date`: Date when an admin marked this survey valid for inclusion in the
  `library`.
* `Status`: Draft, ready to validate, validated, ??? (_TODO_: Better to use date fields
  instead? e.g. a submitted response has `submitted_date` populated, a draft does not)


### Response subjects

Response subjects exist both as a definition in the `registry` and an instantiation with
rating(s) and other fields associated with a `response`. The following specifications
pertain to rated instances, _not_ `registry` definitions.

Some field definitions that may apply to multple subjects:

* `Performance rating`: 0-100 rating of the performance of the subject
* `Criticality rating`: 0-100 (or less) rating of the criticality of an input to an output,
    e.g. criticality of an `observing system` to a `data product`. Rating must not be
    greater than the `performance rating` of the ouptut subject.
* `Rationale`: Why a `criticality` or `performance` rating was selected.
* `Gaps`: Areas where improvement is needed.


#### Observing system

The optional input to a `Data product` (e.g. reanalysis or model-derived data products
may not require an observing system).

Fields/relationships:

* `Performance rating`
* `Rationale` for performance rating
* `Gaps`
* `Data product(s)` supported by this observing system
    * `Criticality rating`
    * `Rationale` for criticality rating


#### Data product

* `Performance criteria`: Text description of what the ideal performance of this data
  product looks like. (_TODO_: Needs more thought. There is some disagreement on the AON
  side about how/if this should be used.)
* `Performance rating`
* `Rationale` for performance rating (_NOTE_: AON team to consider if pre-defined values
  are a good idea.)
* `Gaps`
* `Application` supported by this data product (always the same for a given survey,
  since each survey corresponds with exactly 1 application)
    * `Criticality rating`
    * `Rationale` for criticality rating


#### Application

* `Performance criteria`: Text description of what the ideal performance of this data
  product looks like.
* `Performance rating`
* `Rationale` for performance rating
* `Gaps`


#### Societal Benefit Area (SBA)

This response subject will be completed by an `SBA cohort`.

* `Rationale` of performance rating
* `Gaps`
* `Application` being rated in association with this SBA:
  * `Performance rating`
  * `Rationale` of performance rating
  * `Criticality rating`
  * `Rationale` of criticality rating


### Application survey

Gather information about a single `application` and its related `data products` and
their related `observing systems`.


### Societal Benefit Area survey

Gather information about Societal Benefits of an application. Related to exactly 1
`Application survey`.

This type of survey generally requires input from a larger group. For example, a SBA
survey may be sent to up to ~20 `experts` known as a `societal benefit cohort` and
request information about how 1-3 specific `SBAs` relate to the `application`. Multiple
SBA surveys will be needed to fill out all societal benefits of an application.


## Analysis

A visualization that is generated from the `library` of responses by an `Analyst`
selecting filters based on fields of `response subjects`, such as `tags`. We envision
being able to blend `responses` around common Objects or Fields within those Objects, for
example: "show all `responses` tied to a given `data product`". Or "show all where `tags`
include 'rivers'", etc. If this is overly complex, it can be a down the line feature, but is
critical to how we envision the tool being used over time.

* `Name`: Unique
* `Description`
* `Analyst`
* Filter criteria or list of `responses` associated with the analysis. (_TODO_: If we
  don't want an analysis to change over time, we should probably link it to `reponses`
  by ID. But if we _do_ want the analysis to be automatically updated as more
  `responses` are submitted with e.g. a specific `tag`, we should use filter criteria)


## User personas / roles

### Admin

A user who creates a `survey` and invites `experts` to respond, in addition to
validating `responses` and marking them valid/complete.

When creating a `survey`, the admin either creates or selects an `application` in the
registry to associate with the survey.

Can create `surveys` by creating new `versions` of old surveys.

Fields/relationships:

* Name
* Surveys created


### Expert

A user who is invited to register to provide a `response` to a `survey`. Admins will
assign Surveys to Experts. Experts can contribute to multiple Surveys; Surveys can have
many Experts. We could potentially still circumvent the need for user accounts with the
Admin-driven link system that you originally suggested. We’d just want to capture this
information about the Experts.

Experts do _not_ add new `applications` to the `registry`, but may either select or add
new `data products` and `observing systems` to the `registry`.

Fields/relationships:

* Name
* OrcID (optional?)
* Biography
* Affiliation (should this be saved on a response-by-response basis? Affiliation may
  change between surveys)
* `Tags` of interest (areas of expertise, e.g. `river-watch`)
* `Responses` submitted


### Analyst

A user who registers to generate one or more `analysis`. Eventually, we’d like Analysts
to be able to save their Analyses, recreate them and update them. I’m not sure we need
or should track things like Orcid ID, Bio, Affiliation for Analysts, but we could give
them option. It would help with our analytics.

We might also need to support a Guest Analyst so someone could do visualizations without
registering. If we don’t want to create user accounts, then basically everyone would be
a Guest Analyst and they could just export .jpgs and JSON to recreate their analyses.

Fields/relationships:

* Name
* OrcID (optional?
* Biography
* Affiliation
* Tags of interest (areas of expertise, e.g. `river-watch`)
* `Analyses` submitted


### SBA Rating Cohort

A group of `experts` who provide `responses` to `Societal Benefit surveys`. A cohort
will generally be solicited to complete many `Societal Benefit surveys`, focusing on a
small number of `SBAs`, to provide a view of the societal benefits of many
`applications`.

Fields/relationships:
* `Name`: Unique
* `Description`
* `Expert(s)`: Members of cohort
* `SBA(s)`: SBAs cohort must score
