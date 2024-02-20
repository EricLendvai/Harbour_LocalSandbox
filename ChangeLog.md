# Harbour_LocalSandbox - Change Log

## 02/19/2024 v 1.5
* Code refactor to use Harbour_EL instead of Harbour_VFP.

## 11/01/2023 v 1.4
* Fix to ignore request to resource files, like the favicon.ico.
* Requires Harbour_FastCGI 1.7+

## 04/08/2023 v 1.03
* Changed Dockerfile of devcontainer to work around git install failure introduced around April 2023.

## 02/15/2023 v 1.03
* Simplified linking of libraries hb_el and hb_orm. Update those related libraries.

## 02/10/2023 v 1.02
* Fixed make files to handle updated Harbour_EL.

## 01/29/2023 v 1.01
* Clean up of tasks.json to be smaller and remove "Soft Task Kill" and fix "Del Build Cache" under powershell.
* Added support to calling function in hbunix under linux (devcontainer) and hbwin under windows.

## 01/04/2023 v 1.00
* Port from LocalSandbox Example of the Harbour_FastCGI repo/project
* Added devcontainer support, using Ubuntu 22.04

