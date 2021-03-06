node-checkr
=========

**Note: This client is in alpha stage**

Node Checkr is an unofficial, promise-based client for interacting with the [Checkr.io](https://checkr.com/) platform.

Documentation for the Checkr API can be found [here](https://docs.checkr.com/).

### Getting started


```bash
yarn add node-checkr
```

Create a new account with Checkr and get you `API_key` from you account's settings.


```javascript
import checkr from 'node-checkr';
const Checkr = new checkr(API_KEY);
```

### Objects
- [Candidates](#candidates)
- [Screenings](#screenings)
- [Packages](#packages)
- [Reports](#reports)




Candidates
-----------

##### `list()`

Returns the list of all existing candidates.

```javascript
  checkr.Candidates
    .list()
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `retrieve(id)`

Retrieves a particular candidate, given the `id`.

```javascript
  checkr.Candidates
    .retrieve(id)
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `create(params)`


Creates a candidate do run screenings on. Required parameters might change with the screening to be run. Check the official docs for details.

Supported params:

|         Param         |      Type     | Required |     Notes     |
|:---------------------:|:-------------:|:--------:|:-------------:|
| first_name            | string        |     x    |               |
| middle_name           | string        |          |               |
| last_name             | string        |     x    |               |
| email                 | string        |     x    |               |
| phone                 | alpha-numeric |          |               |
| zipcode               | alpha-numeric |          |               |
| dob                   | string |          | date of birth |
| ssn                   | alpha-numeric |          |               |
| driver_license_number | string |          |               |
| driver_license_state  | string |          |               ||

```javascript
  checkr.Candidates
    .create({
      first_name: 'John',
      middle_name: 'Smith',
      email: 'j.doe@gmail.com',
      last_name: 'Doe',
      dob: '1970-01-22',
      driver_license_number: 'F211165',
      driver_license_state: 'CA'
    })
    .then(candidate => console.log(candidate))
    .catch(err => console.log(err));
```

##### `update(id, params)`

Updates a candidate's information, given the `id`. Same params as `createCandidate`.

```javascript
  checkr.Candidates
    .update('ABC123', {
      first_name: 'John',
      last_name: 'Doe',
    })
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

Screenings
-----------

##### `ssn_trace(id)`

Retrieves an existing SSN trace.

```javascript
  checkr.Screenings
    .ssn_trace('ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `sex_offender(id)`

Retrieves an existing Sex Offender search.

```javascript
  checkr.Screenings
    .sex_offender('ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `global_watchlist(id)`

Retrieves an existing global watchlist search.

```javascript
  checkr.Screenings
    .global_watchlist('ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `national_criminal(id)`

Retrieves an existing national criminal search.

```javascript
  checkr.Screenings
    .national_criminal('ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `county_criminal(id)`

Retrieves an existing county criminal search.

```javascript
  checkr.Screenings
    .county_criminal('ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `state_criminal(id)`

Retrieves an existing state criminal search.

```javascript
  checkr.Screenings
    .state_criminal('ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `motor_vehicle(id)`

Retrieves an existing Motor Vehicle Report.

```javascript
  checkr.Screenings
    .motor_vehicle('ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `education_verifications(id)`

Retrieves an existing education verification.

```javascript
  checkr.Screenings
    .education_verifications('ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `employment_verifications(id)`

Retrieves an existing employment verification.

```javascript
  checkr.Screenings
    .employment_verifications('ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

Packages
-----------

##### `list()`

Returns the list of packages available on your account.
```javascript
  checkr.Packages
    .list()
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `retrieve(id)`

Retrieves a particular package, given the `id`.
```javascript
  checkr.Packages
    .retrieve('ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `create(params)`


Creates a package. Required parameters might change, check the official docs for details.

Supported params:

|         Param         |      Type     | Required |
|:---------------------:|:-------------:|:--------:|
| name            | string        |     x    |            
| slug           | string        |      x    |               
| screenings             | Array(screenings)        |     x    ||

```javascript
  checkr.Packages
    .create({
      name: 'Motor Vehicle Report',
      slug: 'mvr_only',
      screenings: [{ type: 'motor_vehicle_report', subtype: null }]
    })
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

Reports
-----------
##### `retrieve(id)`

Retrieves a particular report, given the `id`.
```javascript
  checkr.Reports
    .retrieve('ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `create(package_slug, candidate_id)`


Creates a report for the candidate specified, using the package.


```javascript
  checkr.Reports
    .create('mvr_only', 'ABC123')
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

##### `update(id, params)`


Updates a report.

Supported params:

|         Param         |      Type     |
|:---------------------:|:-------------:|
| package            | string        |           
| adjudication           | string        |       
Either package or adjudication is required.          

```javascript
  checkr.Packages
    .update('ABC123', {
      package: 'mvr_only'
    })
    .then(res => console.log(res))
    .catch(err => console.log(err));
```

To do
-----------

* Tests for screenings [ ]


Testing & Development
-----------

* Clone repository

```bash
  git clone https://github.com/franciscofsales/node-checkr.git
```

* Install dependencies

```bash
  yarn install
```

* Setup API Key

- copy `.env.example` into `.env` and input your API key.

* Run test set

```bash
  yarn run test
```

Develop and keep tests green.

**NOTE: packages cannot be created multiple times with the same slug, take that into account on package related tests.**


License
-----------

This Library is licensed under the MIT license.
