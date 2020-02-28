# ScandiPWA Documentation

ScandiPWA is a single page application (SPA) theme for Magento with advanced PWA capabilities.

ScandiPWA is based on React and utilizes GraphQL API of Magento 2.3. The problem which our solution solves and the motivation behind the chosen technology stack can be found in the [introduction to ScandiPWA Technology Stack](./introduction.md).

Implementing the SPA is challenging. There are multiple limitations which must be addressed when going for CSR. Find out more about [SPA application challenges](./challenges.md).

Our solution is not the only one providing the SPA experience in the Magento ecosystem. To understand the main differences between the existing solutions, refer to [How we are different?](./existing-solutions.md) section of the documentation.

## Ready to try?

ScandiPWA is a theme for Magento 2. It can be [installed using composer on existing Magento instance](./setup/on-existing-m2.md).

Often, we do not have Magento 2 installed on our local host, or we do not want to install something manually - in that case, we have a docker setup ([for linux](./setup/docker/linux.md), [for mac](./setup/docker/mac.md), and [for windows](./setup/docker/windows.md)).

> **Note**: we strongly recommend setting up using docker. Why? Because it allows us to exclude the environment-related issues from possible reasons when debugging & looking for solutions. There is a whole [FAQ](./setup/docker/faq.md) for most common docker-setup related issue.

In case you would like to use docker setup in production - [see following guide](./setup/docker/production.md).

In case you just want to run ScandiPWA locally using your remote server as a back-end, please follow [this instruction](./setup/with-remote-m2.md).

**The other way to get the ScandiPWA instance** - is to contact hello@scandipwa.com. We can provide you with scalable (production grade) ScandiPWA cloud setup with or without code access, multiple environments (dev, stage, prod), support and more!

If you still have questions regarding installation, please [join our community chat](https://join.slack.com/t/scandipwa/shared_invite/enQtNzE2Mjg1Nzg3MTg5LTQwM2E2NmQ0NmQ2MzliMjVjYjQ1MTFiYWU5ODAyYTYyMGQzNWM3MDhkYzkyZGMxYTJlZWI1N2ExY2Q1MDMwMTk) or open issues in [scandipwa/scandipwa-base](https://github.com/scandipwa/scandipwa-base) repository.

## Discover a theme

ScandiPWA is fast, light-weight and simple to work with. We are claiming this, because we chose the technology stack on the front-end very carefully. Read more about the technologies we utilized in the [front-end technology stack](./theme/tech-stack.md).

A lot of thought is put it the organization of the project internals. The approaches to file structure, file naming, and class naming patterns can be found in the [guide to stay organized](./theme/structure.md).

There are [tools for VSCode](https://github.com/scandipwa/scandipwa-development-toolkit) and broad utility function list in the core of ScandiPWA. Read the [development guide](./theme/dev-guide.md) to speed up the development process.

Finally, for a deep dive into the theme architecture and build configuration refer to the [technical specification](./theme/tech-spec.md).

## Dive deeper into docker setup!


