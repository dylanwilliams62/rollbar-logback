Rollbar Logback
=============

This is a fork of the ahaid's [Rollbar Logback Appender](https://github.com/ahaid/rollbar-logback) for use with the error aggregation service [Rollbar](https://rollbar.com/). 

Notable additions:
- custom fingerprinting mechanism because Rollbar doesn't allow to customize it enough
- a way to sanitize http headers (e.g. to get rid of security tokens)
- more stuff is sent to rollbar
- various small fixes

Logback
------------

	<appender name="ROLLBAR" class="com.tapstream.rollbar.RollbarAppender">
        <apiKey>[YOUR APIKEY HERE]</apiKey>
        <environment>local</environment>
    </appender>

	<root level="debug">
		<appender-ref ref="ROLLBAR"/>
	</root>

Appender parameters:

* url: The Rollbar API url. Default: https://api.rollbar.com/api/1/item/
* apiKey: The rollbar API key. Mandatory.
* environment: Environment. i.e. production, test, development. Mandatory.


Custom MDC parameters
----------------------

Any MDC values with keys that do not start with `RollbarFilter.REQUEST_PREFIX` will be added as custom parameters to
the Rollbar item request.


Servlet Filter
---------------

Located at `com.tapstream.rollbar.logback.RollbarFilter` is a J2EE servlet filter that will populate the `request`
portion of the Rollbar item from a ServletRequest. The filter will include:

* Remote IP address
* User agent
* Method
* URL
* Query String
* Headers
* Parameters


Acknowledgements
--------------

This library has been inspired by:

* [rollbar-java](https://github.com/rafael-munoz/rollbar-java)
* [rollbar-logback](https://github.com/ahaid/rollbar-logback)

