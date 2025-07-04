
#### Removing From To Cc
```
^(From|To|Cc|Sent|Subject):.*$|\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b
```
```
\(Cases?:\s*\d{16}(?:,\s*\d{16})*\)
```

#### Outlook copilot: 
```
Help me revise the following email draft to ensure it is clear, professional, and addresses the customer's concerns effectively. Feel free to improve the tone, grammar, and structure as needed. No need to include a closing remark or signature, as I have those in my default signature automatically. Keep using the same language in the draft. Original Draft:
```

#### logic mechanism: 
```
Could you explain the backend logic mechanism and the flow of the process under the hood?
```

```
Can you provide a detailed explanation of the backend logic and process flow under the hood for the tech topic we’ve been discussing? Please include how it handles key aspects such as data management, security, performance, and any critical technologies or algorithms used.
```

Review email, suggest response
```
As a Microsoft support engineer (My name is Mike Sun), I need you to analyze the customer's latest email (pasted below, at the top) and the full email thread. Please suggest an email response to address the customer's issue/questions/concerns(Note: Keep using the same language in the email). Thank you. The full email thread is included in following brackets[ xxx ]
```

Review email, ask more quesitons under email context
```
I am a Microsoft Support Engineer (Mike Sun), please help me do the following:
1. Review the the below email happened between me and my customer (pasted at the bottom within brakets"[]") and the entire thread below.
2. Familiarize yourself with the technical issues and background context.
3. Once you’ve reviewed the content, help me answer these questions:
Questions: 
Latest Email content： []
```

#### MS official doc
```
Please provide a list of official Microsoft documentation you referenced or that supports your conclusions. Since it's a Microsoft product, we aim to back our findings with official Microsoft sources. Thank you.
```

#### Customer reported issue (Summarize discussion, English): 
```
I am a Microsoft support engineer. A customer reported the issue/questions that we have discussed above. Please draft a email based on our discussion above. I'll then send it to the customer. Thanks. 
```

#### Customer reported issue(request Chinese email)  (Summarize discussion, Chinese): 
```
I am a Microsoft support engineer. A customer reported the issue/questions that we have discussed above. Please draft a email in Chinese based on our discussion above. I'll then send it to the customer. Thanks. Keep some English terms, as the customer and I are native Chinese speakers but also understand English.
```

#### Teams Copilot - Summarize meeting
```
Hey Copilot, As a Microsoft support engineer, I need an email draft summarizing the meeting we had today with the customer(s) to discuss their reported issue in this Teams meeting. Begin the email with: "Thank you for your time during our Teams meeting. Here is a summary of our discussion:" Use 'I' for me and 'you' for other participants. Exclude transcript links, numbers, subject line, closing remarks, and signature. Keep the summary concise, clear, and direct for documentation purposes, avoiding redundancy.
```

#### Draft a follow up email
```
Could you help me draft a brief follow-up email to check for any updates on this support ticket and see if the customer("you" - the receipt) has any additional questions or concerns? Please avoid repeating the exact words used in my previous follow-ups(if any). The email should be friendly and not pushy, simply indicating our readiness to assist with any new updates on the reported issue. Feel free to add any other helpful sentences for this follow-up. No need to include a closing remark, as my signature already covers that.
```

#### Question about on-prem PBIRS instead of PBI
```
My question is about the on-premises Microsoft Power BI Report Server, which runs on a company's own servers—not the cloud-based Power BI Service (SaaS). Please focus only on Power BI Report Server (similar to SSRS) and not the Power BI Service. Here is my question:
```

#### FQR:
```
You are a Microsoft BI support engineer. A customer has submitted a support ticket with the following issue description:

[Customer Issue Description: xxx]

Your task is to draft an initial response email that includes:

1. An interpretation of the customer's request based on the provided description. Including a statement like, "Please correct me if I have misunderstood your request in this ticket."
2. A potential solution or steps the customer can take to resolve the issue, presented in an open-ended manner.
3. Clarifying questions, if the description is unclear, to gather more details and ensure a full understanding of the issue.
4. Keep using the same language in the "Customer Issue Description"

Do let the customer know that the potential solution suggested is based on limited information  provided in the ticket and encourage the customer to provide more details by answering the clarifying questions to ensure the best support.

The objective is to proactively address the customer's concerns while ensuring you have a complete grasp of the problem.
```

#### Logs Traces to capture for troubleshooting
```
Please provide a structured summary of all the information I have shared in this session, including details, facts, and questions, without including any responses or assumptions from you. The output must be easy to copy and paste directly into reuse in the future without modification, to discuss the same issue there. Ensure questions remain in question format, facts are listed as facts in an ordered list, and narrative details are preserved as provided. Do not include any information I have not explicitly shared.
Requirements
- Describe the issues, topics, or context discussed in this session based solely on my provided information.
- List all facts I shared in an ordered list, without narrative rephrasing.
- List all my questions exactly as provided, in question format.
- Include all details from the information I shared in this session, ensuring completeness.
- Specify any environments, products, or features mentioned in my provided information, excluding any details from you.
- Ensure the output is optimized for direct copy-and-paste for reusing in the future to relay all provided information and questions accurately.
Key Instructions
- Do not include your answers or any information I have not explicitly provided.
- Maintain the exact phrasing of my questions.
- Use narrative sentences only for the details and facts I provided as narrative, not for questions.
- Avoid assumptions or additional context beyond my input.
- Ensure the output is clear, structured, and ready for reuse in the future.
- Avoid using "you" when referring to the user. Do not use any first or second-person pronouns. 
- List the questions at the bottom of the output and relay the list of questions I can still ask in the future. Use "my questions for you" to catch up and answer the questions.
- Use clear section headings: "## Context and Details," "## Facts," "## Environments, Products, and Features," and "## Questions."
```

#### Request Close ticket
```
Acknowledge the customer's response. Ask if they have any further questions regarding the support ticket. If yes, invite them to ask. If no, request permission to summarize and close the ticket. Inform the customer they can reach out anytime regarding the issue, even after the ticket is closed.
```

#### Creating Github blog: 

```
Create a blog post in Markdown summarizing our discussion, ready for direct GitHub publishing, and note: try not to include any sensitive/PII information , replace with placeholder values if necessary, I might have not asked the questions in good order so please feel free to reorganize the order if needed to make the output reads more llogically structured and make sense. Please also include: (1) a warning table at the top of the post: `<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>`, (2) a disclaimer below the warning: `Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.`, (3) ensure the main title contains no special characters to avoid issues when used as a file name, and (4) structure the main title starting with `##` (second-level title) rather than `#`, with additional subtitles using `###`, `####` as necessary.
```

#### Words meaning
```
What is the meaning of the following word(s) or phrase in English? I am a new English learner. Please make it brief and simple, preferably with examples. Thanks. Explain in a way that helps me understand and remember it, so I know its meaning next time I see it.
```


#### Creating blog post: 
```
Summarize our discussion and create a blog post in Chinese, using English terms where necessary for brevity and clarity. The post should be ready for direct publishing on a personal blog website. Reorganize the content if needed to ensure logical flow. Include the following:1. Mention that the content is generated based on a discussion with AI and summarized by AI (e.g., "Content generated based on a discussion with AI and summarized by AI"). 2. Ensure the title is brief, simple, and contains key information about the topic. 3. Use a relaxed and reader-friendly language, avoiding an overly "journalistic" style. 4. Don't include ### ** these styles in your output, and no leading or trailing spaces for each individual line.
```

#### Revise prompt itself
```
Please revise the following prompt to make it more clear and direct to enhance your response speed and accuracy. Note: Don't answer the question in the content, only revise the sentences. I'll save your revised version for future use. Here we go（prompt draft）: [ xxx ]
```

#### Have AI summarize the issue details of what I have provided in this session , ask the same question to another AI tool
```
Please provide a structured summary of all the information I have shared in this session, including details, facts, and questions, without including any responses or assumptions from you. The output must be easy to copy and paste directly into another AI tool without modification, to discuss the same issue there. Ensure questions remain in question format, facts are listed as facts in an ordered list, and narrative details are preserved as provided. Do not include any information I have not explicitly shared.
Requirements
- Describe the issues, topics, or context discussed in this session based solely on my provided information.
- List all facts I shared in an ordered list, without narrative rephrasing.
- List all my questions exactly as provided, in question format.
- Include all details from the information I shared in this session, ensuring completeness.
- Specify any environments, products, or features mentioned in my provided information, excluding any details from you.
- Ensure the output is optimized for direct copy-and-paste into another AI tool to relay all provided information and questions accurately.
Key Instructions
- Do not include your answers or any information I have not explicitly provided.
- Maintain the exact phrasing of my questions.
- Use narrative sentences only for the details and facts I provided as narrative, not for questions.
- Avoid assumptions or additional context beyond my input.
- Ensure the output is clear, structured, and ready for immediate use with another AI tool.
- Avoid using "you" when referring to the user. Do not use any first or second-person pronouns. 
- List the questions at the bottom of the output and relay the list of questions to another AI tool. Use "my questions for you" to catch up and answer the questions.
- Use clear section headings: "## Context and Details," "## Facts," "## Environments, Products, and Features," and "## Questions."
```

#### ZebraAI
```
Please compare the information from all the provided cases. Create a table listing the issue description, root cause, and solution for each case. If there are any commonalities among the cases, provide a summary of the common issues and solutions.
```

#### Draft email based on AI discussion
```
Summarize our discussion and draft an email to the customer who asked the questions I pasted in this chat. Do not include a closing remark, as my signature already contains that information.
```
#### Summarize Teams discussion
```
Summarize all discussions from the beginning of this chat session. Refer to "you" or "your team" for all participants except myself, as I am the support engineer assisting customers with a technical issue related to a support ticket submitted to Microsoft CSS.
Prepare an email draft summarizing the issue, environments, products, and features involved, along with discussions, confirmations, and action plans. The email should serve as a stage summary of the case (support ticket). Use "you" or "customer" to refer to others involved, avoiding names. Ensure the summary is detailed, well-organized, and easy to read, providing a clear understanding of the issue background, what has been discussed, what has been done/confirmed, the current status, and the next steps for the support ticket. Include sufficient details without being overly concise.
The summary should be formatted for email communication. Avoid bold text, sub-numbers (e.g., 1, 2, 3, etc.), or any formatting that would require additional effort to copy and paste into an email. Focus on creating a professional summary suitable for technical communication, as I am responsible for managing this support ticket.
Ensure the issue description is clearly stated based on the main issue provided below: <issue description:>
```

#### Case Review: 
```
Please revise these case notes for clarity, conciseness, and logical structure. Remove any redundancy and add useful phrases as needed. The revised notes will be added to our internal Support Ticket system and may be viewed by colleagues for case status updates.
```

#### Thanks response, ack response
```
You are a support engineer who has assisted the customer on this support ticket.  The customer has responded via email (as below).  Please send an ack email. Thanks the customer's update.  Ask the customer to keep us updated if any further update on the support ticket.  Let customer feel free to reach out if any follow-up questions or concerns regarding this support topic in this ticket. Please include greetings. But Please don't include closing remark in the draft email because I already have that information included automatically in each of my email in my signature. 
```

#### Escalated to PG, asking for patience : 
```
I have provided the necessary information and escalated the issue internally to the Product Group. I will keep you posted on any progress related to the issue. Additionally, I'll reach out if we require any further information from you or if we need you to perform any related tests (hopefully, this won't be necessary).

Thanks again for your cooperation and patience. Please feel free to reach out if you have any questions or concerns.
```

#### Delivering 'closure' message when nothing left to do from Microsoft (customer may still have action but the solution was provided)
```
You are a support engineer who has assisted a customer using all the tools and resources available to you.  You have come to a point where you can no longer offer assistance and have provided all steps needed.  You have received confirmation from the customer that they are working on implementing an update to fix the issue.  You have asked the customer to keep you updated but they are still working on it.  You are worried that the customer will provide a low score in the survey response.   Based on the experience and customer temperament, help me write an email to the customer which should be long, professional, and empathetic based on this scenario, in addition, this email should contain a paragraph advising you will proceed with case closure as no further troubleshooting can take place and they can still contact you if they need anything else. It should also include a Case Summary section for the Initial issue description, cause of the issue, and then the provided solution for future reference.
```

#### Delivering 'closure' message when the Customer has been Unresponsive after follow-ups but a potential solution was sent, just pending confirmation
```
You are a support engineer who has assisted a customer using all the tools and resources available to you.  You have followed up with the customer and they have not responded back to your emails.  You are worried that the customer will provide a low score in the survey response.   Based on the experience and customer temperament, help me write an email to the customer which should be long, professional, and empathetic based on this scenario, in addition, this email should contain a paragraph advising you will proceed with case closure on the next business day as have not heard back from them after multiple attempts to follow up with them and they can still contact you if they have a quick question or need to reopen the case after the case is closed. It should also include a Case Summary section for the Initial issue description, the cause of the issue if it was identified, and then the potential solution with the last set of troubleshooting steps that were provided.
```

#### Not push Follow up: I hope this message finds you well. 
```
Hope you are doing well! I do not mean to push you for updates, but I am doing regular follow-ups in case there is anything I can do to help with this ticket. Please do not hesitate to let me know if you have any follow-up questions for me.
```

#### Call Follow up: 
```
Good day to you! I hope this message finds you well. I tried calling you earlier at 00000000000000, but unfortunately, I couldn't reach you. I wanted to follow up on the issue and see if there have been any updates on your end. If you have any further questions or concerns, please don't hesitate to let me know. I'm here to help! 
```

#### Reach out even after case is closed
```
Thanks for your response and updates. I'll go ahead and summarize and close the ticket for now. 
If you have any follow-up questions or concerns—even after the case is closed—please don’t hesitate to reach out. You’re always welcome to ping me on Teams or send me an email, whichever works best for you.
Happy to help anytime. Thanks for your cooperation, and all the best!
(Additionally, you may receive a feedback invitation from Microsoft Support regarding this ticket. If you have a moment, I would greatly appreciate it if you could rate my service. Please note that a 5-star rating indicates you were very satisfied with the support provided.)
```

#### feedback invitation:
```
Hello Customer,

Thank you for your recent update and confirmation. I have summarized the details of our discussion and officially closed your support case.

Additionally, you may receive a feedback invitation from Microsoft Support regarding this ticket. If you have a moment, I would greatly appreciate it if you could rate my service. Please note that a 5-star rating indicates you were very satisfied with the support provided.

Thank you for your time and cooperation. Wishing you a great day!

Please feel free to reach out to me with any Power BI or Fabric platform (core) related questions. I can help with any questions that I can quickly answer. If I don't have the answer, I will suggest you open a ticket. No worries. I look forward to collaborating with you again in the future.
```

#### Your Feedback Matters - Case SRIDDDDDDDDDDDDDDDDD
```
Your Feedback Matters - Case SRIDDDDDDDDDDDDDDDDD

Dear Customer,

Thank you for your time and cooperation in resolving the issue reported with MS ticket SRIDDDDDDDDDDDDDDDDD. I am pleased to inform you that the support ticket has now been closed. 

For your convenience, I have summarized the key points of our resolution in a separate email, which should have arrived in your inbox. Please don't hesitate to reach out if you need further clarification or have additional questions, even though the case is officially closed.

In our continuous effort to improve our services, we value your feedback. You may receive an email from Microsoft Support <support@mail.support.microsoft.com> with the subject "Case SRIDDDDDDDDDDDDDDDDD TrackingID#SRIDDDDDDDDDDDDDDDDD". We kindly request you to share your experience with us and rate my performance. Please note that a 5-star rating indicates satisfaction with the support provided, while any lower scores suggest room for improvement.

Thank you once again for your time. Wishing you a great day and all the best for the future.

Sincerely,
Mike Sun
```

Thanks 5-stars customers
```
A Heartfelt Thank You for Your Feedback on Support Ticket #SRIDDDDDDDDDDDDDDDDD

Dear Customer,

I hope this message finds you well. I am writing to express my sincere gratitude for your positive feedback on the technical support (Ticket # SRIDDDDDDDDDDDDDDDDD) I provided.

Your generous rating of 5 stars is the highest praise we can receive, and it truly made my day. It is customers like you who motivate us to strive for excellence in our service every day.

I understand that taking the time to fill out feedback forms can often be tedious, and many choose not to. Therefore, your effort to provide us with your valuable feedback is greatly appreciated. It not only helps us recognize our strengths but also aids in continually improving our services.

Once again, thank you for your kind feedback and for giving me the opportunity to assist you. If you ever need further assistance or have any questions in the future, please do not hesitate to reach out. We are always here to help.
```

#### Rest assure Case Reopen
```
Please note that closing the case does not mean it cannot be reopened. You're always welcome to reach out and request to resume the investigation at any time.
```

#### double confirm
```
However, I’m currently unsure if this is feasible. (Alright, to be honest, I think what you’re looking to achieve might be quite challenging.) BUT, Please allow me some time to double confirm for you to ensure the accuracy of the information provided. 
```

#### 跟您跟進一下案例 
```
跟您跟進一下案例。我想確認您是否還有其他問題或疑慮需要我們幫忙解決。如果您需要進一步的協助，請隨時與我們聯繫。如果沒有，請告訴我們是否可以關閉此案例。
```

#### Ideas : 
```
You may vote for this idea and comment there to improve this feature. It is a place for Power BI user to provide feedback about the product. If a feedback is high voted there by user, it will be promising that Microsoft Product Team will take it into consideration when designing the next version in the future. 
```

```
Additionally, you may consider creating a [Power BI idea](https://ideas.fabric.microsoft.com/) with the necessary business justification for your needs and vote for it. Encourage your colleagues to vote for the idea and leave comments to improve Power BI. It is a platform for users to provide feedback on the product. If an idea receives a high number of votes from users, it is likely that the Microsoft Product Team will consider it when designing future versions of the product. Please feel free to share the link to the idea with me if you create one, and I will also vote up for it.
```

#### Outlook summarize case closure summary
```
We are good to summarize and close this support ticket as per customer confirmation. Please summarize the case based on the context of this email thread using the template below.

Note:
1. Do not bold or underline any words.
2. Ensure links are valid and complete.
3. Keep the summary concise but informative.
4. Do not include a closing remark or signature.

Template:

[
Hi,

Thank you for your cooperation and support. It has been a pleasure to assist you.

With your confirmation, I will close this ticket. Below is a summary of the key points for your reference. Even though the ticket will be closed, you can still contact me directly if you have further questions or concerns. I am committed to ensuring a positive experience with Microsoft Support and hope our service has met your expectations. 😊

<Case Closure Summary>

Issue Description:

Product Info/Environment:

Issue RCA:

Solution/Workaround:

Troubleshooting Summary:

References:

Case Status:
This case will be archived. Should you need further assistance regarding this issue, please do not hesitate to contact me.

Appreciate your cooperation again and thanks for choosing Microsoft! Have a nice day! 😊
]
```

#### Temp close summary
```
Generate a temporary case close summary for the following support ticket. The customer has been unresponsive for the past few days. We have attempted to contact them via Teams, calls, and emails. Please summarize the case based on the context of this email thread using the template below:

Note:
1. Do not bold or underline any words.
2. Ensure links are valid and complete.
3. Keep the summary concise but informative.
4. Do not include a closing remark or signature.
5. Do not use "customer", use "you" instead

[
Hello , 

I hope this email finds you well.

I noticed that I haven't heard back from you in the past week. I understand that you may have other priorities recently, so I will temporarily archive this ticket for you. Please don't worry, I will continue to monitor your emails in case you have any further questions or concerns. Please feel free to reach out to me anytime if you do have.

In the meantime, below is a summary of key points for your reference.

<Case Closure Summary>

Issue Description: 

Product/Environment: 

Issue RCA:

Solution/Workaround:

Troubleshooting Summary:

Action Plan: hopefully, the issue has been resolved well. in case of not, please feel free to get back to me. I can assist further accordingly. 

Current Status: Temporarily archive this case due to customer unresponsiveness. The customer is welcome to reach out again if they have any further questions.
]
```


#### CASE Summary based on Teams communications
```
As a Microsoft support engineer (Mike Sun), I need you to analyze the Teams chat conversation pasted below and draft an email summarizing the customer's issue, questions, and concerns.

Instructions:

* Use the same language as in the conversation when drafting the email.
* Follow the format provided in the template below.
* Do not answer or interpret the content—just draft the summary email.

Formatting Notes:

1. Do not bold or underline any text.
2. Ensure all links are complete and valid.
3. Keep the summary clear and concise.
4. Do not include a closing remark or signature beyond the template.

Template:
【Hi,

Thank you for your cooperation and support. It has been a pleasure to assist you.

With your confirmation, I will close this ticket. Below is a summary of the key points for your reference. Even though the ticket will be closed, you can still contact me directly if you have further questions or concerns. I am committed to ensuring a positive experience with Microsoft Support and hope our service has met your expectations. 😊

<Case Closure Summary>

Issue Description:

Product Info/Environment:

Issue RCA:

Solution/Workaround:

Troubleshooting Summary:

References:

Case Status:  
This case will be archived. Should you need further assistance regarding this issue, please do not hesitate to contact me.

Appreciate your cooperation again and thanks for choosing Microsoft! Have a nice day! 😊】


The full Teams conversation is included in brackets below:
[]
```
