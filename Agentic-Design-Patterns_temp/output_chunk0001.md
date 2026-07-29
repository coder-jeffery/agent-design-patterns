[智能体设计模式]

 

[*构建智能系统的实践指南*] [安东尼奥·古利] [目录 - 共 424 页 = 1+2+1+1+4+9+103+61+34+114+74+5+4 11 ]

[[题献](https://docs.google.com/document/d/1cQ61mNpiWn6eSORmWjEjF44vN2Lpba8kyKmNwIC60ig/edit?usp=sharing)][, 1 页 ]

[[致谢](https://docs.google.com/document/d/1u2y6tY48bw8nriDUuwWEf9s8g66vyIqBKSKZDOS-n0s/edit?tab=t.0#heading=h.y1l1kh7vu0qi)][, *2 页* ][终稿，已完成最后审读]

[[序言](https://docs.google.com/document/d/18Q9kfZuCTL37ztrSjLxwf8Elr5UfAiAavmnj0IqSpbU/edit?tab=t.0#heading=h.5wi2c0amdd0f),] 1 页 [终稿，已完成最后审读]

[[思想领袖视角：权力与责任](https://docs.google.com/document/d/1PWhaXD_UNKgJaxYe3JBxRFRt3_B8Wm67CFxtSBQ4LkU/edit?tab=t.0#heading=h.2v348nrvaqww)] [终稿，已完成最后审读]

[[引言](https://docs.google.com/document/d/1K5jwqB6jh20uHL0TTWxqWOxFk-dzFxRvHzrRRV79hrg/edit?tab=t.0),] 4 页 [终稿，已完成最后审读]

[[是什么让 AI 系统成为「智能体」？](https://docs.google.com/document/d/1Nw6hRa7ItdLr_Tj5hF2q-OH8B_uPKb--RLn8SXZKA94/edit?usp=sharing)][, 9 页 [终稿，已完成最后审读]

 

[第一部分，（共计：103 页） ]

[1. ] [[第 1 章：提示链](https://docs.google.com/document/d/1flxKGrbnF2g8yh3F-oVD5Xx7ZumId56HbFpIiPdkqLI/edit?usp=sharing)]（[[代码](https://colab.research.google.com/drive/15XCzDOvBhIQaZ__xkvruf5sP9OznAbK9)]），12 页 [终稿，已完成最后审读，代码正常]

[2. ] [[第 2 章：路由](https://docs.google.com/document/d/1ux_n8n3T4bYndOjs1DKW5ccpC802KISdy2IWnlvYbas/edit?tab=t.0)]（[[代码](https://drive.google.com/drive/u/0/folders/1Y3U3IrYCiJ3E45Z8okR5eCg7OPnWQtPV)]），13 页 [终稿，已完成最后审读，代码正常]

[3. ] [[第 3 章：并行化](https://docs.google.com/document/d/1XVMp4RcRkoUJTVbrP2foWZX703CUJpWkrhyFU2cfUOA/edit?tab=t.0)]（[[代码](https://drive.google.com/drive/u/0/folders/1Y3U3IrYCiJ3E45Z8okR5eCg7OPnWQtPV)]），15 页 [终稿，已完成最后审读，代码正常]

[4. ] [[第 4 章：反思](https://docs.google.com/document/d/1HXXJOQIMWowtLw4WMiSR360caDAlZPtl5dPPgvq9IT4/edit?tab=t.0#heading=h.a7nkedxjnyap) ]（[[代码](https://drive.google.com/drive/u/0/folders/1Y3U3IrYCiJ3E45Z8okR5eCg7OPnWQtPV)]），13 页 [终稿，已完成最后审读，代码正常]

[5. ] [[第 5 章：工具使用](https://docs.google.com/document/d/1bE4iMljhppqGY1p48gQWtZvk6MfRuJRCiba1yRykGNE/edit?usp=sharing)]（[[代码](https://drive.google.com/drive/u/0/folders/1Y3U3IrYCiJ3E45Z8okR5eCg7OPnWQtPV)]），20 页 [终稿，已完成最后审读，代码正常]

[6. ] [[第 6 章：规划](https://docs.google.com/document/d/18vvNESEwHnVUREzIipuaDNCnNAREGqEfy9MQYC9wb4o/edit?usp=sharing)]（[[代码](https://drive.google.com/drive/u/0/folders/1Y3U3IrYCiJ3E45Z8okR5eCg7OPnWQtPV)]），13 页 [终稿，已完成最后审读，代码正常]

![](images/000037.jpg)

[献给我的儿子布鲁诺，]

 

[两岁的你，为我的生命带来了全新而耀眼的光芒。当我探索那些将定义我们明天的系统时，我最先想到的，是你将继承的那个世界。]

 

[献给我的儿子莱昂纳多与洛伦佐，以及我的女儿奥萝拉，]

 

[你们已成为出色的女性与男性，正在建设一个美好的世界，我心中充满骄傲。]

 

[这本书讲述如何构建智能工具，但更是献给一种深切的希望：愿你们这一代以智慧与慈悲引导它们。未来无比光明——对你们、对我们所有人皆是如此——只要我们学会用这些强大的技术服务人类、推动进步。]

[致谢]

 

我想向使本书得以成书的众多个人与团队，表达衷心的感谢。

 

首先，我感谢 Google 坚守其使命、赋能 Googlers，并尊重创新的机会。

 

我感激首席技术官办公室（Office of the CTO）给予我探索新领域的机会，坚守其「实用魔法」（practical magic）的使命，并具备适应新兴机遇的能力。

 

我要向我们的副总裁威尔·格兰尼斯致以衷心感谢，感谢他对我自 1994 年最初兴趣以来的信任；也感谢李·布恩斯特拉在提示工程方面的出色工作。

 

我还要感谢 5 Days of GenAI 团队，包括对我们团队给予信任的副总裁 Alison Wagonfeld、始终交付成果的 Anant Nawalgaria，以及展现行动力与领导力的 Paige Bailey。

 

我也深深感谢 Mike Styer、Turan Bulmus 与 [Kanchana Patlolla]，帮助我在 Google I/O 2025 上发布了三个智能体。感谢你们付出的巨大努力。

 

我想向托马斯·库里安表达诚挚的谢意，感谢他在推动云与 AI 举措中坚定不移的领导力、热情与信任。我也深深感谢 Emanuel Taropa，他鼓舞人心的「敢做」态度使他成为我在 Google 遇到的最杰出的同事，树立了真正深远的榜样。最后，感谢 Fiona Cicconi 与我关于 Google 的那些引人入胜的讨论。

Jain、Aldo Pahor、Gaurav Verma、Pavithra Sainath、Mariusz Koczwara、Abhijit Kumar、Armstrong Foundjem、Haiming Ran、Udita Patel 与 Kaurnakar Kotha。

 

没有你们，这个项目绝无可能实现。一切功劳归于你们，一切错误归于我。

 
