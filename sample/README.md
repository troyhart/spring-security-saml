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

### Debugging

Set the environment variable `MAVEN_OPTS` as shown below to enable remote debugging.

    export MAVEN_OPTS=-agentlib:jdwp=transport=dt_socket,address=8000,server=y,suspend=n

See [How to set agentlib property for mvn tomcat plugin (jpda)](http://stackoverflow.com/questions/12422125/how-to-set-agentlib-property-for-mvn-tomcat-plugin-jpda), on stackoverflow, for more information.

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

    https://idp.ssocircle.com:443/sso/saml2/jsp/idpSSOInit.jsp?metaAlias=/publicidp&spEntityID=urn:troyhart:nwri

So this feature has stopped working. I've done some debugging and I can see that the code does pickup `http://idp.ssocircle.com` as the `EntityId`. It picks this
up from the issuer name of the from the SAML message. Debugging, I've found the following two methods that are responsible for parsing/decoding the the message and
coming up with the bad `EntityId`:

* org.opensaml.saml2.binding.decoding.BaseSAML2MessageDecoder.extractEntityId(Issuer)
* org.springframework.security.saml.metadata.CachingMetadataManager.getEntityDescriptor(String)

I suspect that if the sample application were deployed on `https` this issue would go away, but I haven't embarked on this endeavor yet. 


#### TESTSHIB

    https://idp.testshib.org/idp/profile/SAML2/Unsolicited/SSO?providerId=urn:troyhart:nwri

## Guides

* http://docs.spring.io/spring-security-saml/docs/current/reference/html/chapter-quick-start.html