## Error Class

If an error occurs in an FGC method, the error class of the Fresvii.GamingCloud.Models namespace will be returned in the relevant delegate.
The error codes are defined below, followed by the descriptions of the properties.

### Fields

	 public enum ErrorCode
        {
            Unknown = -1,
            NotInitialized,
            InvalidJson,
            UnableToRegisterNotification,
            NetworkNotReachable,
            InvalidTypeOfKeyValueStore,
            LoacalDatabaseError
        }

### Properties
|Type|Name|Description|
|---|---|---|
|int|Code|Error code (int value of ErrorCode) |
|string|Detail|Error details|
|Method|ToString()|Error string|