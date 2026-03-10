## What was the bug?

The OAuth2 token validation logic in `HttpClient.request()` failed to handle plain object tokens. When `oauth2Token` was a plain object `{ accessToken: "stale", expiresAt: 0 }`, the condition `!(this.oauth2Token instanceof OAuth2Token)` was missing, causing the refresh logic to be skipped.

## Why did it happen?

The original condition only checked for `null` or expired `OAuth2Token` instances:
```typescript
if (!this.oauth2Token || (this.oauth2Token instanceof OAuth2Token && this.oauth2Token.expired))
```

Plain objects are truthy and not `OAuth2Token` instances, so they passed through without triggering refresh.

## Why does your fix solve it?

I added `!(this.oauth2Token instanceof OAuth2Token)` to the condition:
```typescript
if (!this.oauth2Token || !(this.oauth2Token instanceof OAuth2Token) || (this.oauth2Token instanceof OAuth2Token && this.oauth2Token.expired))
```

Now any non-`OAuth2Token` object (including plain objects) triggers token refresh, ensuring only valid token instances are used.

## What's one realistic case your tests still don't cover?

The tests don't cover the case where `oauth2Token` is a different object type (like a string, number, or array) that could cause runtime errors when trying to access token properties.
