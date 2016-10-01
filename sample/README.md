# Spring Security SAML Sample Application

This is a sample SAML2 service provider application. The SP metadata (by default: [sp.xml](src/main/resources/metadata/sp.xml); default Entity ID: `urn:troyhart:nwri`) is configured in the `metadata` bean (see: [securityContext.xml](src/main/webapp/WEB-INF/securityContext.xml)).

## Build

    mvn package

## Deploy

    mvn tomcat7:run

NOTE: see the tomcat plugin configuration in [pom.xml](pom.xml) where the web server port is configured. 

## View metadata

    http://localhost:8181/spring-security-saml2-sample/saml/metadata

## Test SP Initiated

    http://localhost:8181/spring-security-saml2-sample

If IDP Discovery is enabled, you will be redirected to a page where you are presented with a list of identity providers. Select the identity provider and press the `login` button.

## Test IDP Initiated

### SSO Circle

    https://idp.ssocircle.com:443/sso/saml2/jsp/idpSSOInit.jsp?metaAlias=/ssocircle&spEntityID=<configurred SP EntityID>

NOTE: see SP metadata configuration for the SP EntityID.

## Guides

* http://docs.spring.io/spring-security-saml/docs/current/reference/html/chapter-quick-start.html