
# MobSF Configurations

MobSF supports a range of environment variable configurations to customize its behaviour and adapt to various deployment scenarios.
Here is a list of supported environment variables.

## General
- **`MOBSF_DEBUG`**: Enables debug mode when set to `1`.
- **`MOBSF_SECRET_KEY`**: Configure a static django secret.
- **`MOBSF_USE_X_FORWARDED_HOST`**: Enables `X-Forwarded-Host` header support when set to `1`.
- **`MOBSF_USE_X_FORWARDED_PORT`**: Enables `X-Forwarded-Port` header support when set to `1`.
- **`TIME_ZONE`**: Configure a timezone for the server, defaults to `UTC`.
- **`MOBSF_PLATFORM`**: Specify the operating environment for MobSF, such as `docker`.
- **`MOBSF_HOME_DIR`**: Specify MobSF home directory to store analysis data, defaults to `~/` or `$HOME`.

## Database Configuration
PostgreSQL is configured only if the required environment variables are set; otherwise, MobSF defaults to using the sqlite3 database.
- **`POSTGRES_USER`**: Username for the PostgreSQL database.
- **`POSTGRES_PASSWORD`**: Password for the PostgreSQL database.
- **`POSTGRES_PASSWORD_FILE`**: Path to a file containing the PostgreSQL password (docker secrets mount).
- **`POSTGRES_HOST`**: Hostname or IP address of the PostgreSQL server.
- **`POSTGRES_PORT`**: Port for connecting to the PostgreSQL server (default: `5432`).
- **`POSTGRES_DB`**: Name of the PostgreSQL database (default: `mobsf`).

## Asynchronous Scan Queue
- **`MOBSF_ASYNC_ANALYSIS`**: Enables asynchronous analysis when set to `1`. This is used to support Async task queues with DjangoQ2.
- **`MOBSF_ASYNC_WORKERS`**: No of asynchronous scans supported at a time, default to 3 workers.
- **`MOBSF_MULTIPROCESSING`**: Specifies multiprocessing mode (`billiard`, `thread`, `default`).

## Tool Timeouts
- **`MOBSF_JADX_TIMEOUT`**: Timeout in seconds for JADX operations (default: `1000`).
- **`MOBSF_SAST_TIMEOUT`**: Timeout in seconds for static analysis (default: `1000`).
- **`MOBSF_BINARY_ANALYSIS_TIMEOUT`**: Timeout in seconds for binary analysis (default: `600`).

## Authentication and Rate Limiting
- **`MOBSF_DISABLE_AUTHENTICATION`**: Disables authentication when set.
- **`MOBSF_RATELIMIT`**: Rate limit for API requests (default: `7/m`).
- **`MOBSF_API_ONLY`**: Enables REST API-only mode when set to `1`. The Web UI endpoints will be disabled.
- **`MOBSF_API_KEY`**: Set a custom static authentication key for MobSF REST APIs.
- **`MOBSF_API_KEY_FILE`**: Read REST API authentication key from a file (docker secrets mount).

## Proxy Configuration
- **`MOBSF_PROXY_IP`**: IP address for the HTTPS proxy run by MobSF(httptools) (default: `127.0.0.1`).
- **`MOBSF_PROXY_PORT`**: Port for the HTTPS proxy run by MobSF(httptools) (default: `1337`).

## Upstream Proxy Settings
- **`MOBSF_UPSTREAM_PROXY_ENABLED`**: Enables upstream proxy support when set to `1`.
- **`MOBSF_UPSTREAM_PROXY_SSL_VERIFY`**: Verifies SSL for upstream proxy when set to `1`.
- **`MOBSF_UPSTREAM_PROXY_TYPE`**: Type of upstream proxy (default: `http`).
- **`MOBSF_UPSTREAM_PROXY_IP`**: IP address for the upstream proxy (default: `127.0.0.1`).
- **`MOBSF_UPSTREAM_PROXY_PORT`**: Port for the upstream proxy (default: `3128`).
- **`MOBSF_UPSTREAM_PROXY_USERNAME`**: Username for upstream proxy authentication.
- **`MOBSF_UPSTREAM_PROXY_PASSWORD`**: Password for upstream proxy authentication.

## Static Analysis Configuration
- **`MOBSF_DOMAIN_MALWARE_SCAN`**: Enables domain malware scan, defaults to `1`.
- **`MOBSF_APKID_ENABLED`**: Enables APKiD scan, defaults to `1`.
- **`MOBSF_DYLIB_ANALYSIS_ENABLED`**: Enables dylib analysis, defaults to `1`.
- **`MOBSF_SO_ANALYSIS_ENABLED`**: Enables shared object analysis, defaults to `1`.
- **`MOBSF_DEX2SMALI_ENABLED`**: Enables dex to smali conversion for Android binaries, defaults to `1`.
- **`MOBSF_PERM_MAPPING_ENABLED`**: Enables permission to code mapping for Android scans, defaults to `1`.
- **`MOBSF_NIAP_ENABLED`**: Enables NIAP scan when set to `1`. This is disabled by default.
- **`MOBSF_CVSS_SCORE_ENABLED`**: Show CVSSV2 scores when set to `1`. This is disabled by default.

## Dynamic Analysis Configuration
- **`MOBSF_ANALYZER_IDENTIFIER`**: Android Debug Bridge (adb) compatible device identifier.
- **`MOBSF_FRIDA_TIMEOUT`**: Frida connection timeout, defaults to `4` seconds.
- **`MOBSF_ACTIVITY_TESTER_SLEEP`**: Wait defined seconds before invoking an activity, defaults to `4` seconds. This is used by Activity tester.
- **`MOBSF_ADB`**: Specify the path to the `adb` binary that MobSF should use for Android dynamic analysis.

## VirusTotal Integration
- **`MOBSF_VT_ENABLED`**: Enables VirusTotal integration when set to `1`.
- **`MOBSF_VT_API_KEY`**: API key for VirusTotal integration.
- **`MOBSF_VT_UPLOAD`**: Enables file uploads to VirusTotal when set to `1`. Otherwise, only hash values are sent to VirusTotal.

## Corellium Integration
- **`MOBSF_CORELLIUM_API_DOMAIN`**: API domain for Corellium integration.
- **`MOBSF_CORELLIUM_API_KEY`**: API key for Corellium integration.
- **`MOBSF_CORELLIUM_PROJECT_ID`**: Project ID for Corellium integration (optional).

## AppMonsta Integration
- **`MOBSF_APPMONSTA_API`**: AppMonsta API key to fetch package details

## SAML SSO Integration
- **`MOBSF_IDP_METADATA_URL`**: Metadata URL for SAML IdP.
- **`MOBSF_IDP_ENTITY_ID`**: Entity ID for SAML IdP.
- **`MOBSF_IDP_SSO_URL`**: Single Sign-On (SSO) URL for SAML IdP.
- **`MOBSF_IDP_X509CERT`**: X.509 certificate for SAML IdP.
- **`MOBSF_IDP_IS_ADFS`**: Set ADFS as IdP when set to `1`.
- **`MOBSF_SP_HOST`**: Hostname for SAML Service Provider (SP).
- **`MOBSF_SP_ALLOW_PASSWORD`**: Enables password-based login for SAML SP when set to `1`.

## Misc
- **`EFR_01`**: Enables a custom enterprise feature request when set to `1`.
