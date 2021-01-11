# ParSecDB  

ParSecDB is a collection of human readable security advisories parsed semi-automatically into machine readable format.

# Why does this thing even exist ? 

![image](https://user-images.githubusercontent.com/28975399/104148266-9b273e80-53f7-11eb-9ed7-5765db710189.png)

When making tools which improve open source security, the bulk of time is spent in converting human readable data into machine readable data. To maintain an advantage w.r.t data, this is done in private. Work is duplicated !

To prevent this, ParSecDB  publicly curates and shares this data under free and libre  license. 

This would have the following benefits: 

1.  **Better tooling:** Open source security tooling would become more accessible, since data is one of the biggest barrier to entry.
2. **Better Resource Allocation:** Currently every security tooling providers, like snyk, nexus etc spend bulk of their resources on collecting and parsing data. ParSecDB takes this out of the equation, thus sparing resources to solve other important problems like :  Is the vulnerable code even called ? 
3. **Better open source adoption:**  Security is one of the most common argument  against open source software adoption, especially in large organisations. With (1) and (2) this won't be the case. 

# The working :

ParSecDB  listens to various sources of security advisories. When new advisories are published, they are then added to queue. These would then be passed through a  parser which would obtain certain vulnerability primitives. The community then reviews and enriches the data via a web app. Upon approval this repository would be updated with the new vulnerability data.

In the early stages, ParSecDB would listen to [apache announces](http://mail-archives.apache.org/mod_mbox/www-announce/) mainly due to the high impact projects it covers and nature of advisories. 

# Data Schema

This is a first draft, and open for better alternatives: 

```
{
	"vulnerability_id" : "CVE-2020-17515",
	
	"vulnerable_packages":[
		"pkg:pypi/apache-airflow@1.10.12",
		"pkg:pypi/apache-airflow@1.10.11",
	]
	
	"unaffected_packages":[
		"pkg:pypi/apache-airflow@1.10.14"
	]
	
	"notes": "The 'origin' parameter passed to some of the endpoints like '/trigger' was vulnerable to XSS exploit."
	
	"references": [
		"https://nvd.nist.gov/vuln/detail/CVE-2020-17515",
		"http://mail-archives.apache.org/mod_mbox/www-announce/202012.mbox/%3CCAH5JyZrtawoGzRYWO%2BCicB9FY5DM740%2BRxDmt2pEn_fM3TctLw%40mail.gmail.com%3E",
	]
}
```

**Note:**  Packages are represented using package urls, because they make it easy to represent packages of different ecosystems together.  See [purl-spec](https://github.com/package-url/purl-spec) to learn more about package urls. 



