# Web Penetration Testing Cheatsheet

### Important
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP testing guide](https://owasp.org/www-project-web-security-testing-guide/)
- [The WASC Threat Classification v2.0](http://projects.webappsec.org/w/page/13246978/Threat%20Classification)

- `curl -i IP` Inspect headers using -v(verbose output) or -i
- `curl -X OPTIONS Domain.com -i` Check if PUT, DELETE, MOVE are accepted

### Checks
1. Client side validation
2. Database interaction
3. File upload/download
4. Display of user input
5. Redirections
6. Access control and Login protected pages
7. Error messages - Status codes (404,403,5xx)

### Extensions and Files
- `bak, bac, old, 000, 001, ~, 01, _bak, inc, Xxx`
- Files: `.git, .htaccess, robots.txt`

### XSS
### SQLi
- [https://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet](https://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet)
- Sqlmap `sqlmap -u "http://ip/sqli_1.php?title=hello&action=search" --cookie "PHPSESSID=m42ba6etbktfktvjadijnsaqg4; security_level=0" -p title`
