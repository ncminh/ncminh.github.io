---
layout: post
title: Useful Powershell scripts for AD
---

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

![_config.yml]({{ site.baseurl }}/images/config.png)

![_config.yml]({{ site.baseurl }}/images/first-post.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.

Test the syntax highlight:

```js
function testfunc(a, b) {
  if (a === b) {
    return true;
  }
  return false;
}
```



Export all users with selected properties to CSV file

```powershell
Get-ADUser -filter * -properties * | select-object name,emailaddress, enabled, department, passwordlastset | export-csv -path c:\userexport20210512_1518.csv
```



** Disable/Enable a list of users from csv file:

```powershell
# $name = "test02"

$namelist = Import-Csv C:\names.csv

# foreach($name in $namelist) { Disable-ADAccount -Identity $name }
# foreach($name in $namelist) { Write-Output $name.Name }

foreach($user in $namelist) { Disable-ADAccount -Identity $user.Name }

######################################################################


$namelist = Import-Csv C:\names.csv

# foreach($name in $namelist) { Disable-ADAccount -Identity $name }

# foreach($name in $namelist) { Write-Output $name.Name }
foreach($user in $namelist) { Enable-ADAccount -Identity $user.Name }
```



