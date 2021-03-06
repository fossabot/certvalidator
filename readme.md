# certvalidator
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2FMatthiasValvekens%2Fcertvalidator.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2FMatthiasValvekens%2Fcertvalidator?ref=badge_shield)


A Python library for validating X.509 certificates or paths. Supports various
options, including: validation at a specific moment in time, whitelisting and
revocation checks.

 - [Features](#features)
 - [Related Crypto Libraries](#related-crypto-libraries)
 - [Current Release](#current-release)
 - [Dependencies](#dependencies)
 - [Installation](#installation)
 - [License](#license)
 - [Documentation](#documentation)
 - [Continuous Integration](#continuous-integration)
 - [Testing](#testing)
 - [Development](#development)
 - [CI Tasks](#ci-tasks)


[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2FMatthiasValvekens%2Fcertvalidator.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2FMatthiasValvekens%2Fcertvalidator?ref=badge_large)

## Features

 - X.509 path building
 - X.509 basic path validation
   - Signatures
     - RSA, DSA and EC algorithms
   - Name chaining
   - Validity dates
   - Basic constraints extension
     - CA flag
     - Path length constraint
   - Key usage extension
   - Extended key usage extension
   - Certificate policies
     - Policy constraints
     - Policy mapping
     - Inhibit anyPolicy
   - Failure on unknown/unsupported critical extensions
 - TLS/SSL server validation
 - Whitelisting certificates
 - Blacklisting hash algorithms
 - Revocation checks
   - CRLs
     - Indirect CRLs
     - Delta CRLs
   - OCSP checks
     - Delegated OCSP responders
   - Disable, require or allow soft failures
   - Caching of CRLs/OCSP responses
 - CRL and OCSP HTTP clients
 - Point-in-time validation

Unsupported features:
 
 - Name constraints

## Related Crypto Libraries

*certvalidator* is part of the modularcrypto family of Python packages:

 - [asn1crypto](https://github.com/wbond/asn1crypto)
 - [oscrypto](https://github.com/wbond/oscrypto)
 - [csrbuilder](https://github.com/wbond/csrbuilder)
 - [certbuilder](https://github.com/wbond/certbuilder)
 - [crlbuilder](https://github.com/wbond/crlbuilder)
 - [ocspbuilder](https://github.com/wbond/ocspbuilder)
 - [certvalidator](https://github.com/wbond/certvalidator)

## Current Release

0.11.1 - [changelog](changelog.md)

## Dependencies

 - *asn1crypto*
 - *oscrypto*
 - Python 2.6, 2.7, 3.2, 3.3, 3.4, 3.5, 3.6, 3.7, 3.8 or pypy

## Installation

```bash
pip install certvalidator
```

## License

*certvalidator* is licensed under the terms of the MIT license. See the
[LICENSE](LICENSE) file for the exact license text.

## Documentation

[*certvalidator* documentation](docs/readme.md)

## Continuous Integration

Various combinations of platforms and versions of Python are tested via:

 - [AppVeyor](https://ci.appveyor.com/project/wbond/certvalidator/history)
 - [CircleCI](https://circleci.com/gh/wbond/certvalidator)
 - [GitHub Actions](https://github.com/wbond/certvalidator/actions)
 - [Travis CI](https://travis-ci.org/wbond/certvalidator/builds)

## Testing

Tests are written using `unittest` and require no third-party packages.

Depending on what type of source is available for the package, the following
commands can be used to run the test suite.

### Git Repository

When working within a Git working copy, or an archive of the Git repository,
the full test suite is run via:

```bash
python run.py tests
```

To run only some tests, pass a regular expression as a parameter to `tests`.

```bash
python run.py tests path
```

### PyPi Source Distribution

When working within an extracted source distribution (aka `.tar.gz`) from
PyPi, the full test suite is run via:

```bash
python setup.py test
```

### Test Cases

The test cases for the library are comprised of:

 - [Public Key Interoperability Test Suite from NIST](http://csrc.nist.gov/groups/ST/crypto_apps_infra/pki/pkitesting.html)
 - [OCSP tests from OpenSSL](https://github.com/openssl/openssl/blob/master/test/recipes/80-test_ocsp.t)
 - Various certificates generated for TLS certificate validation

## Development

To install the package used for linting, execute:

```bash
pip install --user -r requires/lint
```

The following command will run the linter:

```bash
python run.py lint
```

Support for code coverage can be installed via:

```bash
pip install --user -r requires/coverage
```

Coverage is measured by running:

```bash
python run.py coverage
```

To install the packages requires to generate the API documentation, run:

```bash
pip install --user -r requires/api_docs
```

The documentation can then be generated by running:

```bash
python run.py api_docs
```

The following will run a test that connects to all (non-adult) sites in the
Alexa top 1000 that respond on port 443:

```bash
python run.py stress_test
```

Once the script is complete, results that differ between the OS validation and
the *certvalidator* validation will be listed for further debugging.

To change the version number of the package, run:

```bash
python run.py version {pep440_version}
```

To install the necessary packages for releasing a new version on PyPI, run:

```bash
pip install --user -r requires/release
```

Releases are created by:

 - Making a git tag in [PEP 440](https://www.python.org/dev/peps/pep-0440/#examples-of-compliant-version-schemes) format
 - Running the command:

   ```bash
   python run.py release
   ```

Existing releases can be found at https://pypi.org/project/certvalidator.