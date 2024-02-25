# One-liners

One-liner grabs OS version info, timezone, uptime, number of users, etc. caption = OS Name, csname = hostname:

{% code overflow="wrap" %}
```
wmic os get buildnumber, version, caption, countrycode, csname, currenttimezone, description, installdate, lastbootuptime, localdatetime, muilanguages, name, numberofusers, osarchitecture /format:list
```
{% endcode %}

One-liner grabs same as above but with domain/workgroup info, hypervisor present, roles, username, etc:

{% code overflow="wrap" %}
```
wmic computersystem get bootupstate, caption, currenttimezone, description, dnshostname, domain, domainrole, hypervisorpresent, initialloadinfo, installdate, name, partofdomain, roles, username, workgroup /format:list
```
{% endcode %}
