# Spring Security SAML Sample Application

This is a sample SAML2 service provider application. The [security context configuration](src/main/webapp/WEB-INF/securityContext.xml)
specifies a bean named `metadata` which configures the metadata for one service provider and two
identity providers. 

## Service Provider (SP) Metadata

* EntityID: [urn:troyhart:nwri](src/main/resources/metadata/sp.xml)

## Identity Provider (IDP) Metadata

* EntityID: [https://idp.ssocircle.com](src/main/resources/metadata/ssocircle-idp.xml)
* EntityID: [https://idp.testshib.org/idp/shibboleth](src/main/resources/metadata/testshib-idp.xml)

## Build

    mvn package

## Deploy

    mvn tomcat7:run

NOTE: see the tomcat plugin configuration in [pom.xml](pom.xml) where the web server port is configured.


## View metadata

    http://localhost:8181/spring-security-saml2-sample/saml/metadata

## Testing

You need to have an account on SSO Circle and/or TESTSHIB to be able to test.

### SP Initiated

    http://localhost:8181/spring-security-saml2-sample

If IDP Discovery is enabled, you will be redirected to a page where you are presented with a list of 
identity providers. Select the identity provider and press the `login` button.

Also, you can trigger login and identify the IDP with the following URL: `http://localhost:8181/spring-security-saml2-sample/saml/login?idp=<IDP EntityID>`

### IDP Initiated

See [SP metadata configuration](src/main/resources/metadata/sp.xml) for the SP EntityID. By default, the value will be: `urn:troyhart:nwri`


#### SSO Circle

    https://idp.ssocircle.com:443/sso/saml2/jsp/idpSSOInit.jsp?metaAlias=/ssocircle&spEntityID=urn:troyhart:nwri

#### TESTSHIB

    https://idp.testshib.org/idp/profile/SAML2/Unsolicited/SSO?providerId=urn:troyhart:nwri

## Guides

* http://docs.spring.io/spring-security-saml/docs/current/reference/html/chapter-quick-start.html