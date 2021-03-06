# ServiceNow Localization

This repo contains everything you need to get started with Localization in ServiceNow with resources and code samples for beginners.

> Where should I even start?

The Phases of Localization in ServiceNow:

1. Before you Start - Plan the Localization Strategy
2. When you Start - Find Missing Translations
3. Somewhere in the Middle - Establish Design and Development Standards
4. After Go-Live - Test the Localization Implementation
5. In the Future - Maintain the Localization Implementation

Here's the link to our Knowledge CreatorCon 2022 Session: **Five things I wish I knew before attempting to localize my scoped application** so you can learn more about these different phases! [[LINK]](https://knowledge.servicenow.com/newyork/sessiondetail?sessionId=1647877774150001sdwQ&sessionTimeId=1649454667893001f5Q0&state=k22newyork.sessiondetail&redirect_uri=https%3A%2F%2Fknowledge.servicenow.com%2Flibrary) 
(You can also check out the slides here. [[LINK]](/Five%20things%20I%20wish%20I%20knew%20before%20attempting%20to%20localize%20my%20scoped%20application.pptx))

## Contents

While the slides presented a high level overview of these different localization phases, the following contents are intended to go more in depth with additional explanations and examples.

### Find Missing Translations:

Our tool: [Clear Skye I18N Scanner Utility](https://developer.servicenow.com/connect.do#!/share/contents/5449480_clear_skye_i18n_utility?v=1.0&t=PRODUCT_DETAILS) - We are using this to help us dig up all those pesky strings in our scripts, but we made it after we recorded our session so we didn't get to talk about it. Oh well - now we have a topic for next year! 

- [Debug Translations](/Debug%20Translations.md) - learn how to find missing translations.
- [FetchCode](/FetchCode.md) - learn how to use the FetchCode tool to search for hard-coded strings.
- [Locate translatable strings](/Locate%20translatable%20strings.md) - learn how to create stub translation records needed for custom translations.

### Establish Design and Development Standards:

- [Design and Development Standards](/Design%20and%20Development%20Standards.md) - follow these best practices to make it easier to localize custom strings.
- [Custom Translations](/Custom%20Translations.md) - learn how to translate custom strings.

## Resources

- [Internationalization & Localization Community Forum](https://community.servicenow.com/community?id=community_forum&sys_id=494156411baef850c17111751a4bcbca)

To learn more, check out:

- [Custom translations](https://docs.servicenow.com/en-US/bundle/sandiego-platform-administration/page/administer/localization/concept/translating-applications.html)
- [Employee Center Academy: Localization and Multi-language Support](https://www.youtube.com/watch?v=IMIx40Jnfvo)
- [Hard-coded strings are bad, mmmkay](https://community.servicenow.com/community?id=community_article&sys_id=ef6c2a761bf73050ed6c9979b04bcb36)
- [How do you choose what languages to offer?](https://community.servicenow.com/community?id=community_article&sys_id=bccf651cdbfb305080073ca8f496195b)
- [In-Platform Language Support Guide](https://community.servicenow.com/community?id=community_blog&sys_id=4f0023711b22bc9017d162c4bd4bcb03)
- [Return a message in a specific language, gs.getMessageLang()](https://community.servicenow.com/community?id=community_article&sys_id=fcebed42db8dfc10d58ea345ca9619b9)
- [Solution design is just as important as translations](https://community.servicenow.com/community?id=community_article&sys_id=045d58241b44c590ed6c9979b04bcb38)
- [Support your globalization with well-planned localization](https://www.servicenow.com/content/dam/servicenow-assets/public/en-us/doc-type/success/workbook/globalization-localization.pdf)

## Contributing

Have something you think should be included here? Let us know!
