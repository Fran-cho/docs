#Authentication

The API is statless and every request that requires special permissions must be authenticated separarely with HTTP Basic Authentication headers over SSL. You can test out your authentication by visiting `yourorganization.ada.support/api/` with your username and a sha3_256 hash of your password in the authentication header. You should be returned your client (organization) and your user object in the response.

```py

# Working example:
auth_try = requests.get(
  url="https://test.ada.support/api/",
  auth=("david", "36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80")
)

print auth_try.json() # > {u'message': u'Hello david'...
```
