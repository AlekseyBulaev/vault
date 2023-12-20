## Why Custom Actions?
[doc](https://docs.github.com/en/actions/creating-actions/about-custom-actions)

Simplify workflow steps
- instead of writing multiple (possibly very complex) step definitions, we can build and use a single custom action
- multiple steps can be grouped into a single custom action
No existing (community) action
- existing, public actions might not solve the specific problem we have in our workflow
- custom action can contain any logic we need to solve our specific workflow problems
---
## Different Types of Custom Actions

JavaScript Actions
- execute a JavaScript file
- use JavaScript (NodeJS) + any packages of our choice
- pretty straightforward 
Docker Actions
- create a dockerfile with our required configuration
- perform any task(s) of our choice with any language
- lots of flexibility but requires Docker knowledge
Composite Actions
- combine multiple workflow steps in one single action
- combine run (commands) and uses (actions)
- allows for reusing shared steps (without extra skills)
---
[url](https://docs.github.com/en/actions/creating-actions)
![[Pasted image 20231125230808.png]]

---
## JavaScript Action

[doc](https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action)

```BASH
npm install @actions/core
npm install @actions/github
```

```JS
const core = require('@actions/core');
const github = require('@actions/github');

try {
  // `who-to-greet` input defined in action metadata file
  const nameToGreet = core.getInput('who-to-greet');
  console.log(`Hello ${nameToGreet}!`);
  const time = (new Date()).toTimeString();
  core.setOutput("time", time);
  // Get the JSON webhook payload for the event that triggered the workflow
  const payload = JSON.stringify(github.context.payload, undefined, 2)
  console.log(`The event payload: ${payload}`);
} catch (error) {
  core.setFailed(error.message);
}
```
---
