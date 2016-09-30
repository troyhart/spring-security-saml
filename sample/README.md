# Spring Security SAML Sample Application

This application is configurred for the ssocircle service provider with metadata id of: com.nwri.n4e

## Build

mvn package

## Deployment

mvn -Dmaven.tomcat.port=8181 tomcat7:run

## View metadata

http://localhost:8181/spring-security-saml2-sample/saml/metadata

## Test SP Initiated

Open the front page of your SP application (http://localhost:8181/spring-security-saml2-sample/), select `http://idp.ssocircle.com` IDP and press login.

## Test IDP Initiated

Point the browser to ssocircles and reference the configurred SP EntityID: `https://idp.ssocircle.com:443/sso/saml2/jsp/idpSSOInit.jsp?metaAlias=/ssocircle&spEntityID=com.nwri.n4e`

## Guides

* http://docs.spring.io/spring-security-saml/docs/current/reference/html/chapter-quick-start.html
* 