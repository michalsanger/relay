# Unreleased

# 3.2.0

- New bin script `kiwicom-fetch-schema` available. This little script helps you with the download of your remote schema. Please, read README file to see how to use it.

# 3.1.0

- Flow types of some object types are now more accurate
- Reverted breaking change enforcing correct Environment usage from version 3.0.0

# 3.0.0

- _(reverted in 3.1.0)_ Breaking: functions `commitMutation`, `requestSubscription` and `commitLocalUpdate` now require correct usage of Relay environment which is being passed down from props. Example of how to properly use mutations:

```js
import {
  type RelayProp, // or `PaginationRelayProp` or `RefetchRelayProp` types
} from '@kiwicom/relay';

type Props = {| +relay: RelayProp |};

function Component(props: Props) {
  useEffect(() => {
    commitMutation(
      props.relay.environment, // <<< this Environment is not being imported but rather reused from `props.relay`
      { mutation: graphql` ... ` },
    );
  });
}
```

- Relay updated to version 5.0, see: https://github.com/facebook/relay/releases/tag/v5.0.0
- This release also contains new _experimental_ Relay Compiler with support for persistent queries. This is currently undocumented feature and you should not use it. Expect breaking changes without any announcements.

# 2.3.0

- You can now pass custom GraphiQL Printer into Relay environment factory. There is a default printer enabled for https://graphql.kiwi.com/ - you can just click on the GraphiQL link in your dev console and it will open current query with variables so you can debug it easily.

# 2.2.0

- Experimental Flow support for operation loader (needed for `@match` and `@module`).

# 2.1.0

- Babel Relay preset is now part of this package. Removed from `@kiwicom/babel-preset-kiwicom` in version 3.0.0. Please, edit your Babel configuration files (example for Next.js applications):

```js
module.exports = {
  presets: ['@kiwicom/babel-preset-kiwicom', 'next/babel'],
  plugins: ['relay'],
};
```

# 2.0.0

- Upgraded to Relay version 4.0.0 (see: https://github.com/facebook/relay/releases/tag/v4.0.0). Our previous versions 1.x disallowed some deprecated usages of Relay so this upgrade should be relatively straightforward. Check new testing tools in this release - especially `MockPayloadGenerator` and `RelayMockEnvironment`. There is also an improved support for `@match`/`@module` directives (available from `@kiwicom/relay` version 1.0) which works well with `@kiwicom/babel-preset-kiwicom` from version 3.0. Please give it a try and give us your feedback.

# 1.2.0

- Network fetcher now accepts optional `refetchConfig` to be able to adjust `fetchTimeout` and `retryDelays` (see for more details: https://github.com/kiwicom/fetch)

# 1.1.0

- `Disposable` Flow type exposed publicly
- `Environment` (incomplete) Flow type exposed publicly
