# Changelog

All notable changes to this project are documented in this file. See
[Conventional Commits](https://conventionalcommits.org) for commit guidelines.

# 1.0.0 (2025-09-04)


### Bug Fixes

* Adress the IPA server by its FQDN for successful disenrollment ([01b56d8](https://github.com/ewcloud/ewc-ansible-role-ipa-client-disenroll/commit/01b56d81f3e21273d8d7df16ca51fdb671a3be98))


### Features

* Add disenrollment logic for external DNS setups, including fallback method for Ubuntu 24 ([46e5cde](https://github.com/ewcloud/ewc-ansible-role-ipa-client-disenroll/commit/46e5cde122702a3137c97c2bcc1380f7ca6ccc5a))
* Add host and DNS disenrollment logic, including fallback methos for Ubuntu 24 ([3049f67](https://github.com/ewcloud/ewc-ansible-role-ipa-client-disenroll/commit/3049f67fb61313667d1cc93a5f9fc644752c039b))
* Gather facts about IPA client installation ([5daa787](https://github.com/ewcloud/ewc-ansible-role-ipa-client-disenroll/commit/5daa7872c4c19dd952df3fc49031a993846d3bc9))
* Prevent credential leaks into logs upon task failure ([214bba7](https://github.com/ewcloud/ewc-ansible-role-ipa-client-disenroll/commit/214bba787b62b6f2e0324dd4cc2b9fd1e9460b57))
* Validate that runtime is within supported Linux distributions ([06a39a6](https://github.com/ewcloud/ewc-ansible-role-ipa-client-disenroll/commit/06a39a608a9b9ff3db936aeedcc01ed1ff1e6bf0))
