# How to get `NVM install` to work when ssl certs are possibly bad

## Problem

When trying to install a node version using NVM **on a mac**:

```Bash
GovernmentHack@ myProject % nvm install
```

But you get the error:

```Bash
Found '/Users/GovernmentHack/Workspace/myProject/.nvmrc' with version <16.20.0>
Version '16.20.0' not found - try `nvm ls-remote` to browse available versions.
```

indicating that the version cannot be found. This is obviously not possible, since that version of NPM is widely used and distributed. The issues can be confirmed by also calling:

```Bash
nvm ls-remote
```

And getting the response:

```Bash
            N/A
```

## Solution

Because the issue is most likely due to an SSL issue, you can export the HTTP distro url like so:

```Bash
export NVM_NODEJS_ORG_MIRROR=http://nodejs.org/dist
```

Then subsequent `nvm install` calls will be successful.
