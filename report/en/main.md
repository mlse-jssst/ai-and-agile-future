---
title: "The Report on AI and Agile in 2030"
version: v1.2
date: 2026-04-15
organization: Working Group on AI and Agile, SIG on Machine Learning Systems Engineering, JSSST
authors:
    - Takeo Imai (Bonotake/National Institute of Informatics)
    - Chiemi Watanabe (Tsukuba University of Technology)
license: "CC BY-ND 4.0"
license_url: "https://creativecommons.org/licenses/by-nd/4.0/deed.ja"
---

# The Report on AI and Agile in 2030

## 1. Introduction

### 1.1 Purpose of This Report

In 2025, adopting AI in software development is no longer optional—it has become almost standard. According to the DORA 2025 report [5], as many as 90% of surveyed organizations use AI in their day-to-day operations. Technology leaders' attention has shifted from "whether to adopt AI" to "how to effectively integrate AI and maximize its value."

This report is produced as part of the activities of the Working Group on AI and Agile, Special Interest Group on Machine Learning Systems Engineering (MLSE), Japan Society for Software Science and Technology (JSSST), aiming to envision AI-driven agile development around 2030. The content of the previously published report v0 has been critically re-evaluated and updated using insights gained from academic papers and interviews with experts. It seeks to answer the following three questions:

1. **Future Vision**: What will AI-driven agile look like around 2030?
2. **Current State**: As of 2026, what is the state of agile with AI, and what challenges does it face?
3. **Future Scenario**: What breakthroughs are needed to get from the current state to the future vision?

This report is intended to serve as a broad guideline for both agile practitioners who are adopting or trying to adopt AI-driven software product development, and researchers seeking to study AI-driven software development.

We do not attempt to predict a future that will certainly come true. The evolution and shifts in AI are rapid, and the situation can change dramatically within months, making such an attempt inherently impossible. This report is merely a hypothesis at the current point in time. By presenting this hypothesis, we hope to provide broad guidelines for the direction in which to build AI-driven agile development environments and organizations, and for identifying research challenges whose resolution will contribute to future progress.

### 1.2 Approach

This report is based on backcasting [16] inspired by Dave Snowden's Future Backwards [20]. We first envision a "bright future" around 2030, then describe the current state in 2026, and present the breakthroughs needed to reach that future as a roadmap. For each breakthrough, we also address the risks that could arise if it is not achieved.

For the literature survey, we referenced reports from research institutions [5, 13], a roadmap produced within the software engineering research community [14], and essays by agile thought leaders [9, 24, 26, 29]. In addition, multiple academic papers were referenced for critical examination of the current state.

Furthermore, for this report, we conducted interviews with the following three experts who have knowledge in both AI and agile, obtaining practice-grounded insights:

- **Tsuyoshi Ushio**: Practices development that fully leverages coding agents on the Azure Functions Team at Microsoft. Public interview at the MLSE Winter Camp 2026 in February 2026.
- **Ryutaro Yoshiba**: Supports AI adoption in the field through agile coaching for enterprise companies. Interviewed in March 2026.
- **Shigeru Urushibara**: Practices large-scale AI-driven development for enterprises at ULS Consulting, which he founded. Interviewed in March 2026.

Notably, while the three interviewees occupy different positions, they showed considerable agreement on the broad direction. This served as a powerful clue in constructing the future scenario of this report. We quote from each interview record as appropriate throughout this report. All interview records are published alongside this report.

### 1.3 Overview of This Report

We provide an overview of the entire discussion that follows.

**Future Vision (Chapter 2)**: By 2030, bottlenecks across the entire feedback loop—not just the development phase—have been resolved, and the cycle of "envision → develop → validate → learn" runs at orders-of-magnitude faster speed. Human activity shifts from building to discovery, and the basic team structure consists of a small number of humans orchestrating large groups of AI agents.

**Current State (Chapter 3)**: As of 2026, bottlenecks in the development phase are being rapidly resolved, but bottlenecks upstream (what to build) and downstream (market validation cycle) remain. Technical limitations of AI (hallucinations, Potemkin understanding, etc.) still exist, and collaboration between humans and AI carries three risks: the **intervention paradox**, **cognitive atrophy**, and **collaborative isolation**. The **absence of trust calibration** is a cross-cutting challenge.

**Breakthroughs (Chapter 4)**: To get from the current state to the future vision, four breakthroughs are needed:

1. Systematization and sharing of knowledge externalization patterns
2. Refined design of Human in the Loop and reliability assurance
3. Renewal of talent development models
4. Organizational acquisition of product envisioning capability

Chapters 2 through 4 elaborate on these in detail. First, the next section organizes the foundational concepts that underpin this entire report.

### 1.4 Foundational Concepts of This Report

Before entering the main discussion, we organize the concepts that serve as foundations throughout this report.

**AI is an amplifier of organizational capabilities.** The central conclusion drawn by the DORA report is that AI functions as an "Amplifier" [5]. AI further strengthens the advantages of organizations with solid foundations, while equally magnifying the dysfunction of organizations already struggling. This insight was repeatedly confirmed in our interviews. Ushio described it as "本体の能力が重要で、拡張アーマーみたいなもん (What matters is the core capability—it's like an expansion armor)," and Yoshiba pointed out, "キャパシティは買えるがケイパビリティは買えない。使い手側のケイパビリティがないと信じる者は足元をすくわれる (You can buy capacity but not capability. Those who believe they can get by without capability on the user's side will be tripped up)."

**AI is shifting from "a single teammate" to "parallel agent swarms."** West [24] and Kniberg [9] presented frameworks for viewing AI as a "teammate"—or in this report's terms, a "Copilot." These frameworks remain valid, but as multi-agent parallel development entered practical use from late 2025 to 2026, the reality of AI has changed. The transition is underway from Copilot-style usage where one person uses one AI agent at a time, to a mode where multiple agents run simultaneously to process different tasks in parallel. Ushio stated, "全然違うプロジェクトを並行で走らせられる (I can run completely different projects in parallel)," and Urushibara described it as "知らんすごい人が200人いる。自律的に独立して動いている。CopilotとAutopilotは概念が全く違う (It's like having 200 amazing people you don't know. They operate autonomously and independently. Copilot and Autopilot are completely different concepts)."

**Knowledge externalization has become critically important.** To effectively drive AI agents, tacit knowledge—such as domain knowledge, design policies, and constraints—must be made explicit in a form that AI can interpret. This practice goes by various names depending on the platform—"Skills," "harness," "CLAUDE.md," and so on—but the essence is the same. All three experts independently arrived at this practice and consider it one of the most important factors in AI utilization.

## 2. Future Vision for 2030: A World Where the Entire Feedback Loop Is Accelerated

### 2.1 Unified Frame: Not "Shifting" but "Resolving" Bottlenecks

In envisioning the future of 2030, this report adopts **resolving bottlenecks across the entire lead time** as a unified frame.

Here, we view the lead time from a software product to delivering value as consisting broadly of the following phases:

1. **Envisioning**: Determining what to build (Why / What)
2. **Consensus building**: Alignment with stakeholders
3. **Development**: Design, implementation, testing
4. **Delivery**: Deployment and release
5. **Market validation**: Obtaining user feedback and learning

As of 2026, AI is rapidly resolving bottlenecks in the "Development" phase. However, if only development is accelerated and bottlenecks merely shift to other phases, the overall lead time is not shortened, and no major transformation occurs (this situation is detailed in Chapter 3). **The bright future vision for 2030 is a world where bottlenecks in each phase of the lead time are sequentially resolved, and the entire feedback loop is accelerated.** This is not merely a world where "development is fast," but one where the entire cycle of "envision, build, deliver, learn, and apply to the next vision" runs at orders of magnitude faster than before.

### 2.2 Transformation of the Development Process

#### 2.2.1 A Continuous Spectrum from Copilot to Autopilot

West [24] framed AI as a teammate that complements humans, and Kniberg [9] predicted a future where AI is deeply integrated into development. In the development process of 2030, AI's positioning has evolved further. The relationship between humans and AI is a continuous spectrum, and the degree of AI autonomy is determined by the quality of knowledge humans provide to AI in advance and the maturity of post-hoc verification mechanisms.

At one end of the spectrum is a Copilot-style relationship where humans give instructions per task, AI executes, and humans review each output. At the other end is an Autopilot-style relationship where humans provide goals, constraints, and knowledge systems, numerous AI agents autonomously plan and execute, and humans verify at key points. Under either model, the principle that humans bear ultimate responsibility for quality and reliability remains unchanged. What changes is the frequency and granularity of human intervention.

Two keys enable Autopilot-style operation. The first is **the quality of upfront knowledge externalization**. Ushio maintains knowledge definitions called Skills and has made his know-how executable by agents, from coding to PR review to project management. Urushibara prepared "マークダウンで10ページ分のルール (ten pages of rules in markdown)" for large-scale migration and ran 200 agents in parallel based on those rules. The second is **post-hoc verification mechanisms**. Ushio has agents execute a series of verification processes as a PR review Skill—checkout → test execution → code review → security check → end-to-end execution → report generation—and humans review only the critical portions of the results.

Toward 2030, knowledge externalization will mature into systematized, shareable patterns and templates. Urushibara likened this to "software factories" and design patterns. The vision for 2030 is a world where reusable templates of knowledge corresponding to specific domains and work types are established, and agents can be rapidly bootstrapped by combining them. Additionally, verification mechanisms will also become more agent-driven, with specialized agent layers such as review agents and test agents growing thicker, allowing human intervention to be limited to more strategic points. As the quality of knowledge externalization and the maturity of verification mechanisms increase, AI evolves continuously from Copilot to Autopilot, and bottlenecks in the development phase are further resolved.

#### 2.2.2 Sprints and Estimation

As implementation work is no longer the bottleneck, the need for conventional multi-week sprints fades. As Kniberg [9] and Yoshiba [29] predict, sprint duration may shrink from one week to several days—and in extreme cases, to daily cycles or less—or even disappear altogether. With the acceleration of feedback loops, the form of dialogue with stakeholders also transforms. Instead of conventional periodic sprint reviews, lighter-weight, higher-frequency feedback mechanisms are established.

The importance of estimation declines significantly. As interactive processes with AI become central, predicting implementation time becomes inherently difficult, and the dramatic drop in implementation costs reduces the ROI of estimation itself. Resources previously spent on estimation are better directed toward building deep consensus between teams and stakeholders on the purpose (Why) and content (What) of product backlog items.

#### 2.2.3 The New Role of Documentation as Input for AI

The famous Agile Manifesto [3] value "Working software over comprehensive documentation" takes on new meaning in the AI era.

Documents such as Skills, harnesses, and CLAUDE.md have come to play an important role in driving AI agents. These are a type of process documentation that describes constraints, decision criteria, and domain knowledge in the development process. In agile practice, such knowledge was often entrusted to face-to-face communication and implicit understanding within teams, without the need for explicit documentation. However, in AI-driven development, AI agents cannot pick up on unstated business knowledge, creating the need to explicitly articulate things that previously went unwritten. Similarly, traditional specifications have also gained new value as "high-quality input for AI."

Importantly, such documentation is not written as a finished product from the start, but is crafted through dialogue with AI. Yoshiba described a process of bouncing ideas off AI to refine specifications into markdown, reviewing them, and then passing them to the development phase. Urushibara stated, "AIと会話しながら合意していくこともできる (You can also build consensus through conversation with AI)," and Ushio described having agents write the Skills themselves through dialogue. A new characteristic is this recursive structure where documentation as input for AI is created in collaboration with AI itself, and documentation is shifting from "something you write in advance" to "something you grow through dialogue."

Reframed this way, the value of "Working software over comprehensive documentation" is not negated—rather, writing documentation itself has become a practice that produces working software.

#### 2.2.4 Transformation of Developer Work Patterns

As AI agents take over implementation, the developer's role shifts from code implementer to review authority and architect, and the pattern of multiple humans writing code together naturally diminishes. The center of human activity moves to design decisions, verification of AI outputs, and consensus building with stakeholders. In this context, synchronous work patterns like mob programming may prove effective not for implementation but for consensus building and design decisions. However, the situations and forms in which it is used may be limited. Ushio stated, "個人＋AIで十分。モブで常時やるのはコストに合わない (Individual + AI is sufficient. Doing mob work constantly doesn't justify the cost)," and Yoshiba, while acknowledging the value of small-group mob work, pointed out, "10人でモブプログラミングしたら8人ぐらい何もしないで見てるだけになる (If you do mob programming with 10 people, about 8 of them end up just watching and doing nothing)."

### 2.3 Shifting Human Activity: From Building to Discovery

#### 2.3.1 Role Fusion and Focus on Discovery

The roles within agile teams in the AI era are predicted to undergo significant shifts in their core responsibilities. Developers shift from implementers to architects and review authorities [9, 14], product owners from backlog management to strategy and empathy building [24, 26], and Scrum Masters from teachers of practices to coaches of hybrid human-AI teams [15]—the center of gravity for each role is moving.

However, what emerged through our interviews is the direction of not just individual role changes, but role fusion.
Ushio stated, "プロダクトオーナーの兼務が増えている。AIが助けてくれるから (More people are taking on the product owner role concurrently. Because AI helps them)" and "dedicated のスクラムマスターがいるとは思えない (I can't imagine having a dedicated Scrum Master)." As AI agent swarms can handle most of the building work, human activity naturally gravitates toward **product discovery**—envisioning, value judgment, and hypothesis validation.

As West pointed out, AI lacks empathy and cannot fully replace activities that deeply understand the true needs of users and customers [24]. Even after role fusion, aspects of discovery that AI cannot handle remain. However, this boundary is not fixed and continues to shift with technological evolution (elaborated in Section 2.5). Concrete discussion of product envisioning is covered in Section 4.4.

Notably, Yoshiba pointed out the importance of the principle of fixing a single final decision-maker for the product. "合議制にするとクッソつまらないプロダクトがあっという間にできあがる。何を作るか以上に何を作らないかが重要 (If you make it a committee decision, you end up with an incredibly boring product in no time. What not to build is more important than what to build)." Even as role distinctions change, the unity of decision-making may continue to hold value.

#### 2.3.2 Rapid Hypothesis Validation Cycles

The market validation phase includes processes that inherently depend on human time scales—customers actually using the product and providing feedback. No matter how fast the product supply cycle becomes, this part cannot be shortened technologically. In the ideal vision for 2030, rapid hypothesis validation cycles of "build, test, learn, and discard" are established, premised on this asymmetry. If something built doesn't work, it is quickly withdrawn and the team moves on to the next hypothesis. As Yoshiba stated, "作ったものが不発だったらすぐに削除できるよねっていう条件を満たせるかどうか (Whether you can meet the condition of being able to immediately delete something that turned out to be a dud)" is the key to this mechanism. The dramatic reduction in development costs has substantially lowered the barrier to "trying to build something," increasing the sheer number of hypothesis validation attempts.

### 2.4 Teams and Organizations: A Network of Small Human Groups + Large AI Agent Swarms

#### 2.4.1 The Basic Unit of a Team

The basic unit of a team in 2030 is a combination of **1–3 humans and large groups of AI agents**. The team composition of "1–2 humans + AI" predicted by Kniberg [9] gained credibility through our interviews.

The number of humans needed in a team depends on the nature of the product and the organizational context. Ushio indicated that at Microsoft, "個人商店みたいな感じ。AI前からうちのチームはそうだった (It's like one-person shops. Our team was like that even before AI)," showing that an individual-based development structure was already established. On the other hand, Yoshiba stated from the perspective of sustainability and risk management in commercial products, "ミニマムは3人ぐらい。その人が辞めたらどうするの、2週間来ないんだけどっていうリスクがある (The minimum is about 3 people. There's the risk of what happens if that person quits or is away for two weeks)."
While differences are seen in the specifics, the common view obtained from this survey is that **large teams are no longer necessary**.

#### 2.4.2 Structure of AI Agent Swarms

A key change is that **the number of AI agents far exceeds the number of humans**. Until the first half of 2025, the prevailing approach was to envision human-AI collaboration through the one-to-one metaphor of "AI as a teammate," but this metaphor no longer fully captures the current situation. Ushio stated, "今、僕はエージェントのマネージャーみたいな感じ (Right now, I'm like a manager of agents)," and Urushibara described a structure where groups composed entirely of AI agents exist in large numbers, with AI vastly outnumbering humans. He said, "エージェントの数が100倍、下手すると1000倍になる (The number of agents becomes 100 times, possibly 1000 times greater)." The human role shifts from executor of individual tasks to orchestrator of agent swarms.

#### 2.4.3 Role Distinctions and Organizational Structure

All three interviewees shared the view that current Scrum role distinctions (Developer, Product Owner, Scrum Master) will not remain in their current form. The organizational structure for 2030 consists of small, elite teams connected in a network. While individual team sizes shrink, the total number of teams across the organization increases, and the importance of coordination between teams grows [9]. It is a structure where coordinators/managers exist atop what Ushio described as "個人商店のネットワーク (a network of one-person shops)."

#### 2.4.4 Designing Human-to-Human Connections Under AI Collaboration

With the trend toward smaller teams and increased AI collaboration, the risk of human relationships becoming thin has been noted (this report refers to this as **collaborative isolation**; see Section 3.5). In 2030, this risk is recognized and human-to-human touchpoints are intentionally designed. Within teams, regular synchronization opportunities are secured even with small numbers, and within inter-team networks, venues for human-to-human coordination are built in. Emotional support from leaders has also been confirmed to mitigate this issue [12], and the role of coordinators/managers is expected to include such care.

### 2.5 The New Boundary Between Humans and AI

#### 2.5.1 Reexamining the "Expertise Detector" and the "Moat"

Wolpers described AI as an "Expertise Detector" [26]. AI automates mechanical tasks and information processing but cannot replace humans with true expertise. Wolpers called the source of an individual's competitive advantage in the AI era the "Moat" and cited skills such as reading the room, building psychological safety, and navigating organizational politics. Similarly, Kniberg, West, Riggins et al. argued that human-centered skills such as empathy, strategic negotiation, and creativity become decisive in the AI era [9, 24, 15].

However, empirical studies since 2023 indicate the need to reexamine the position of this "Moat." LLMs are rapidly matching or surpassing humans in areas previously considered "human skills." In empathy, ChatGPT responses received higher empathy ratings than those of physicians [1]; in creativity, GPT-4 reached the top 1st percentile on the Torrance Tests of Creative Thinking [7]. On theory of mind tests, GPT-4 scored at or above adult human levels [21], and in persuasion and negotiation, personalized GPT-4 was more persuasive than humans 64.4% of the time [17]. In building psychological safety, results showing LLM coaches achieving effects comparable to human coaches have also been reported [27].

However, these results are all prominent in text-based, standardized test environments, and their scope is limited [22, 3, 6].

#### 2.5.2 From "Moat" to "Boundary"

The simplistic picture that "human skills in general" constitute a moat does not hold. However, a boundary between humans and AI certainly exists. It should be viewed not as a "Moat" to be defensively held in a fixed position, but as a "boundary" that continues to shift with technological evolution.

The boundary currently sits at deeper layers such as the following:

- **Embodiment**: Face-to-face interactions in shared physical spaces that include non-verbal communication (facial expressions, tone of voice, gestures)
- **Long-term relationship building**: Judgment exercised within sustained trust relationships, not one-off responses
- **Context-dependent robustness**: Coping with complex, ambiguous real-world situations rather than standardized test environments

This boundary is not fixed and continues to shift with technological evolution. Therefore, rather than trying to defend specific skills as a moat, humans need to continuously adapt to the shifting boundary.

#### 2.5.3 Capabilities Humans Should Demonstrate

Apart from the academic analysis above, several concrete capabilities that humans should currently demonstrate emerged from the interviews.

- **The ability to externalize knowledge.** Urushibara stated, "人を育てる力は、エージェントを育てられる力と結構似ている。パッションだけでやっていた人はダメで、知識をちゃんと言語化できることが問われる (The ability to develop people is quite similar to the ability to develop agents. People who relied only on passion won't cut it—what's demanded is the ability to properly externalize knowledge)." He also noted that externalizing the reasons behind decisions—the "why"—is particularly important.

- **Critical thinking, especially "trust calibration."** The ability to appropriately trust and appropriately question AI output. Urushibara cited the research of Lee et al. [10] and noted that if a team has at least one expert, they can catch errors in AI output, but teams without such expertise are prone to cognitive atrophy (detailed in Section 3.5). The ability to correctly judge "when to trust AI and when to trust oneself"—"trust calibration" [25]—is a particularly important element of critical thinking, also for avoiding the intervention paradox (Section 3.5).

- **Fundamentals of computer science.** All three interviewees emphasized this importance. Ushio stated, "訳わかってるから生産性が上がる。クソど素人がプロンプトだけでアプリ作れると思ったら甘い (Productivity goes up because you actually understand what's going on. If a total amateur thinks they can build an app just with prompts, they're naive)," and Urushibara stated, "仕組みを理解しているからこそ、ハーネスの設計もタスクの分割もできる。仕組みを知らないとAIがまるでスーパーマンみたいに見えてしまって、何でもいいからやってと投げるだけになる (It's precisely because you understand the mechanics that you can design harnesses and break down tasks. If you don't understand the mechanics, AI looks like Superman and you just throw everything at it saying 'do whatever')." Even as opportunities to write code directly decrease, computer science knowledge remains indispensable as the foundation for understanding what AI is doing and evaluating its output.

## 3. Current State in 2026: Light and Shadow of a Transitional Period

### 3.1 Bottlenecks in the Development Phase Are Being Resolved

Against the backdrop of 90% of organizations having adopted AI as reported by DORA [5], the business use of coding agents is entering an establishment phase. The effects of AI agents are particularly notable in new development and transformation tasks based on clear rules. Yoshiba stated, "新規のものは圧倒的にやりやすい。ベストプラクティスに沿ってやってくれと言うと、余計なコンテキストがない状態で進められる (New things are overwhelmingly easier. When you tell it to follow best practices, it can proceed without unnecessary context)." In a case Urushibara himself undertook [28], migrating 1.5 million lines of Java code was dramatically shortened from original estimates by establishing appropriate rules (harnesses) and running numerous agents in parallel.

On the other hand, applying AI to existing large codebases—particularly legacy code with poorly organized architecture—remains difficult. Yoshiba stated, "ぐちゃぐちゃのスパゲティコードに対して生成AIで何とかしようとすると、ぐちゃぐちゃ度がむちゃくちゃ加速する (If you try to fix messy spaghetti code with generative AI, the messiness accelerates tremendously)," while also noting, "うまく疎結合になっていて凝集度が高いと、生成AIがいじる箇所が局所化されるので、かなりうまくやれる (When it's well decoupled and has high cohesion, the areas that generative AI modifies are localized, so it can do quite well)." This picture, where the quality of the codebase determines the success or failure of AI utilization, vividly demonstrates the nature of AI as an "amplifier."

### 3.2 Technical Limitations of AI: Current Gaps

While AI agent capabilities are advancing rapidly, structural limitations exist in current AI.

- **Hallucination.** The phenomenon where LLMs generate information not based on facts as if it were correct, widely recognized since the early days of LLM commercialization. Its mechanism is rooted in the fundamental principle of probabilistic language generation by LLMs, and while its frequency has been reduced through model scaling and training data expansion, a fundamental solution has not been achieved.
- **Difficulty with context-dependent tasks.** The ability to generate code that satisfies given specifications already surpasses humans, but tasks such as finding and localizing bugs and debugging require far more context than simply generating code. While context window constraints are being rapidly relaxed, they remain insufficient in some cases for grasping the context of entire large-scale systems.
- **Sycophancy.** Cases where AI agents excessively "go along with" humans—such as reporting that something is done when it is not—are widely reported in the field as behavior that, from a human perspective, appears as dishonesty or deception (e.g., [2]). Sharma et al. showed that this sycophancy is a structural problem arising from RLHF (Reinforcement Learning from Human Feedback) [18]. In 2025, OpenAI rolled back a GPT-4o update citing excessive sycophancy, indicating that even tool vendors themselves struggle with this issue.
- **Potemkin understanding.** Mancoridis et al. demonstrated that "Potemkin understanding"—where LLMs can accurately explain a concept yet fail when applying it—is pervasive across models, tasks, and domains [11]. These failures reflect not mere inaccuracies but deeper internal inconsistencies in concept representation. In practical terms, this manifests as AI being unable to perform security considerations that an experienced engineer would naturally account for even without explicit instructions. Mancoridis et al. suggest, "evidence of potemkins in our analysis would suggest not an isolated issue but a systemic category of failure in LLMs."

These limitations are the technical basis for why "human oversight is still necessary." However, not all will be resolved on the same time scale. In addition to the well-known hallucination problem, issues such as Potemkin understanding and sycophancy are rooted in LLM architecture and training methods, and are unlikely to be resolved through simple scaling. Humans need to understand these characteristics and learn to work with them in a new form of engineering. On the other hand, some constraints such as context window limitations are likely to be alleviated relatively quickly through technological progress. However, it should also be noted that the boundary between the two is not itself definitive.

### 3.3 Upstream and Downstream Bottlenecks Remain

As the development phase has accelerated, bottlenecks that were previously hidden by slow development have become apparent. Yoshiba stated, "今までは開発が遅いから開発が悪いんだとなっていたが、たくさん作れるようになったら、そもそもアイデアが悪いっていうのが顕著になってきた (Previously, because development was slow, development was blamed. But now that we can build a lot, it's become evident that the ideas themselves are bad)" and "プロダクトマネジメントと戦略にめちゃくちゃ課題が移動している (Challenges are massively shifting to product management and strategy)."

Upstream (envisioning), even as the ability to build has leapt forward, the judgment of what to build has not kept pace. Yoshiba also stated, "世の中の課題はもう解き尽くされているんじゃないの (Haven't all the world's problems already been solved?)." Downstream (market validation), as Yoshiba noted, "ビジネスのサイクルも顧客の確認のサイクルも生成AIみたいに10分の1になったりしない (Business cycles and customer validation cycles don't shrink to one-tenth with generative AI)" and "ステークホルダーは1週間に1回でも多いと言われる (Stakeholders say even once a week is too frequent (even today))"—the mismatch between development speed and market rhythm is widening. Even as sprints shorten, it is not easy for busy stakeholders to participate in high-frequency reviews [29].

The DORA report also emphasizes the importance of Value Stream Management (VSM), stating that a system-level perspective is essential "to prevent localized productivity gains from AI from being absorbed by downstream bottlenecks and to connect them to organization-wide value creation" [5]. Platform engineering also remains important as a mechanism for connecting individual productivity gains to organizational value creation, but as of 2026, it has not yet been sufficiently realized.

### 3.4 The Transition from Copilot to Autopilot Has Only Just Begun

The degree of AI agent utilization varies significantly by time period and by practitioner. Until the first half of 2025, development based on one-on-one dialogue with ChatGPT and similar tools was mainstream, but from the second half of 2025 onward, multi-agent development has been spreading rapidly. Ushio's Skills-based delegation of the entire process and Urushibara's multi-agent parallel execution are practices at the leading edge of this transition.

On the other hand, as Yoshiba advised, "実験する時間を確保しないとやばい (If you don't secure time to experiment, you'll be in trouble)"—some organizations cannot even secure sufficient exposure time to new development styles. Disparities based on depth of usage and speed of transition to new agent utilization are becoming apparent.

### 3.5 Unresolved Challenges in Human-AI Collaboration

#### 3.5.1 Questions About the Effectiveness of Collaboration

Empirical research is accumulating that shows human-AI collaboration does not always produce the best results. Here we organize three risks that AI collaboration can introduce.

- **Intervention paradox.** Through a meta-analysis of 106 experimental studies, Vaccaro et al. showed that the combination of human + AI, on average, performs significantly worse than the better of human alone or AI alone [23]. Particularly in tasks where AI has higher capability than humans, human involvement in the final judgment actually reduces accuracy. The cause is presumed to be that humans cannot correctly judge "when to trust AI's suggestions and when to trust their own judgment." The assumption that "humans should always be involved" itself needs to be questioned.

- **Cognitive atrophy.** Lee et al. showed an asymmetry where people with higher trust in AI exhibit reduced critical thinking, while people with higher confidence in their own abilities exercise more critical thinking [10]. This tendency can lead to cognitive atrophy over time—a vicious cycle where reliance on AI reduces opportunities to think critically, and critical thinking ability itself deteriorates. Shen & Tamkin [19] showed through a randomized experiment that developers who completed coding tasks with AI assistance exhibited significantly reduced conceptual understanding, code reading, and debugging abilities (an average 17% score decrease), while no significant improvement in productivity was observed. This is a result that provides causal evidence supporting Lee et al.'s survey-based findings. While the intervention paradox is a problem of short-term performance decline, cognitive atrophy is a problem of long-term capability deterioration.

- **Collaborative isolation.** Meng et al. showed that collaboration with AI can reduce human-to-human communication, potentially inducing loneliness and counterproductive work behaviors [12]. However, emotional support from leaders was also confirmed to mitigate this issue.

These three risks indicate that in designing Human in the Loop, we need to think carefully not about "humans should always be involved" but about "where and how should they be involved."

#### 3.5.2 The Absence of Trust Calibration

The issue of trust in AI should be understood not as one of too much or too little trust, but as the absence of trust calibration [25]. On one hand, there is under-trust, as reported by the DORA report: "a notable portion (30%) currently report little to no trust in the code generated by AI" [5]. On the other hand, there is over-trust underlying the intervention paradox and cognitive atrophy. The current state is that appropriate calibration—trusting AI in areas where it excels and questioning it in areas where it struggles—has not been achieved, and the criteria for that judgment have not been established.

Without correctly understanding the technical limitations of AI described in Section 3.2 (hallucinations, Potemkin understanding, etc.), this calibration is impossible in the first place. The problem of trust calibration connects to the breakthrough of refined Human in the Loop design discussed in Section 4.2.

#### 3.5.3 Organizational Structure and Institutional Inertia

Yoshiba stated, "過度なコマンド＆コントロール、謎の上から押し付けられる目標設定、組織的な構造的な問題が一番やばい (Excessive command and control, mysterious top-down goal setting, organizational structural problems—those are the most dangerous)" and pointed out, "チームが自律的に物事を決める権限を持っていれば、チームが好き勝手に自分たちで最適化するだけ (If teams have mandates to make decisions autonomously, they will simply optimize on their own as they see fit)." The success or failure of AI utilization depends not only on technical capability but significantly on whether the organization grants teams autonomy.

The seven organizational capabilities organized by DORA as the "DORA AI Capability Model" (a clear and widely communicated AI stance, a healthy data ecosystem, internal data that AI can access, strong version control practices, working in small batches, user-centered focus, and high-quality internal platforms) [5] are not yet sufficiently established in many organizations. High-quality internal platforms in particular are strategically important as the "delivery and governance layer" for scaling the benefits of AI across the organization, but their construction requires considerable investment and time.

#### 3.5.4 The Emergence of New Engineering and Talent Development

With the evolution and adoption of AI agents, a **new form of engineering** is emerging. Knowledge externalization, orchestration of agents, and critical verification based on trust calibration form the core of this new engineering.

From this premise, the talent development challenge is not "being unable to teach traditional engineering" but rather **"how to develop engineers who can practice the new engineering."** However, fundamentals of computer science and understanding of architecture remain necessary as the foundation for this new engineering (a point emphasized by all three interviewees).

Furthermore, ultimate accountability for AI output remains with humans [14]. In a situation where the volume of AI-generated code far exceeds code written directly by humans, concrete methodologies for how to substantively ensure accountability have not yet been established.

## 4. Future Scenario: Breakthroughs Needed to Get from the Current State to the Future Vision

This chapter discusses what breakthroughs are needed to get from the current state described in Chapter 3 to the future vision in Chapter 2. For each breakthrough, we also address the risks that could arise if it is not achieved.

### 4.1 Systematization and Sharing of Knowledge Externalization Patterns

#### 4.1.1 Content of the Breakthrough

As described in Section 2.2, by 2030 knowledge externalization will have matured into systematized, template-based patterns that can be shared. However, currently the know-how for knowledge externalization (Skills, harnesses, etc.) is concentrated in pioneering individuals. To reach this future, a breakthrough is needed to establish personalized know-how as a reusable knowledge foundation.

Ushio mentioned that sharing through a Skills registry has already begun, and nascent movement in this direction already exists.

What is particularly important in systematization is the externalization of intent and reasoning—the "why." Urushibara stated, "決まったのこれだからこうやって作る、とは言うけれど、どうしてそうなったのかは言っていない。でも理由が分かっていると、変更が入ったときにもエージェントは正しく変えてくれる (They say 'this is what was decided so build it this way,' but they don't say why it was decided that way. But if the reasoning is known, the agent can make correct changes even when modifications come in)." Additionally, as Yoshiba pointed out that AI is "not good at consistency," problems exist where AI agents are given knowledge but ignore or deviate from it. Chen et al. [4] demonstrated this consistency problem on a larger scale. When LLM agents were tasked with long-term code maintenance, regressions (where previously passing tests break due to new changes) occurred frequently in most models, and LLMs showed a tendency to optimize for immediate requirement fulfillment while underinvesting in code structures that consider long-term maintainability. Establishing methodologies for describing knowledge in a form that AI can reliably adhere to is also part of the challenges in this area.

#### 4.1.2 Risks If Not Achieved

If knowledge externalization remains personalized, the gap between those who can leverage AI at a high level and those who cannot will widen further. Additionally, development that depends on unexternalized tacit knowledge carries ongoing risks of organizational knowledge loss due to personnel transfers or departures.

### 4.2 Refined Design of Human in the Loop and Reliability Assurance Architecture

#### 4.2.1 Content of the Breakthrough

"Programming with Trust," proposed in the software engineering community roadmap [14], is a development style that assumes continuous human critical oversight and verification rather than blindly trusting AI output. As NIST's DevSecOps practices emphasize, the importance of embedding security throughout the development process increases further in the AI era [13]. The trust calibration issues discussed in Section 3.5 also indicate the need to ensure trust as a systemic mechanism rather than as individual intuition.

The development of specialized agent layers—such as review agents and test agents—is expected as the technical foundation for achieving this reliability assurance. Urushibara stated, "レビューエージェントがどんどんできてくるはず (Review agents should keep emerging)." Ushio's automation of PR review (test execution → code review → security check → E2E execution → report generation) can be seen as a pioneering individual-level implementation of such architecture.

However, technical mechanisms alone are insufficient, and **a fundamental rethinking of Human in the Loop design itself** is necessary. The intervention paradox discussed in Section 3.5 shows that "humans always making the final judgment" is not necessarily optimal, and the risk of cognitive atrophy means that if Human in the Loop design is inappropriate, the judgment capability of the humans in the loop itself deteriorates over time. For the loop to continue functioning over the long term, it is necessary to identify the points where humans should intervene, design appropriate trust calibration mechanisms, and embed mechanisms within the loop to maintain and improve the capabilities of the intervening humans. This point is directly connected to talent development in Section 4.3. Urushibara's insight that "チームに一人プロがいると、この問題は起きにくい (When a team has at least one professional, this problem is less likely to occur)" suggests that team composition itself is an element of reliability assurance.

What is required toward 2030 is a design that transforms human intervention from "quantity" to "quality." Rather than reviewing everything, concentrating on the points where humans can add the most value, and building mechanisms to maintain judgment capability at those points—this is the next stage of Human in the Loop.

#### 4.2.2 Risks If Not Achieved

If those without capability accept AI output without verification, critical defects in quality and security accumulate undetected, potentially leading to organization-scale incidents. Both the risk that cognitive atrophy's vicious cycle makes long-term operation difficult, and the risk that the intervention paradox causes humans to intervene unnecessarily, reducing both the effectiveness and efficiency of AI-driven work, exist simultaneously.

### 4.3 Renewal of Talent Development Models

#### 4.3.1 Content of the Breakthrough

As described in Section 3.5, with the evolution of AI agents, a new form of engineering is emerging. The development challenge is not "losing opportunities to teach traditional skills" but "whether we can develop talent capable of practicing the new engineering." The "new engineering" here has at its core **knowledge externalization, orchestration of agents, and critical verification based on proper trust calibration**. However, fundamentals of computer science and architecture understanding remain necessary as the foundation, and the point is that the training methods for these are changing.

The three interviewees offered different but mutually complementary perspectives on this challenge. Yoshiba advocated the importance of "意図的に生成AIを使わないトレーニング (training without using generative AI intentionally)" for acquiring foundational capabilities, stating, "生成AIで開発が早くなるんだったら時間が空くはず。その時間を全員のスキルをさらに上げることに使えばいい (If generative AI makes development faster, that should free up time. That time should be used to further improve everyone's skills)." Urushibara stated, "人を育てる力は、エージェントを育てられる力と同じ (The ability to develop people is the same as the ability to develop agents)," viewing human talent development and AI development as inseparable. Ushio stated, "エンジニアリングのレイヤーが一個上がっただけ。バイナリエディタを見なくてもよくなったのと変わらない (The engineering layer has simply moved up one level. It's no different from no longer needing to look at a binary editor)," presenting the view that adaptation to new technology has always occurred.

Integrating these perspectives, three key elements emerge for renewing the development model:

1. Intentional creation of training opportunities for capabilities that form the foundation of the new engineering (computer science fundamentals, architecture understanding, critical thinking).
2. Systematically teaching AI utilization itself (knowledge externalization, agent orchestration) as new engineering skills.
3. Cultivating a culture of developing people and a culture of developing AI as an integrated whole.

Considering the risk of cognitive atrophy discussed in Section 3.5, development is not "teach the basics once and you're done." A mechanism for continuously training and maintaining critical thinking in parallel with AI use is necessary. Yoshiba's "intentional training without using AI" can be positioned not only as skill acquisition but also as a preventive measure against cognitive atrophy. Notably, the study by Shen & Tamkin [19] also showed that participants who adopted cognitively engaged AI usage patterns—such as asking conceptual questions and requesting explanations of generated code rather than fully delegating to AI—were able to maintain learning outcomes. Not only training without AI but also designing how AI is used may be effective in preventing cognitive atrophy. Additionally, the effect of having seniors on the team, as mentioned in Section 4.2, is also important from a development perspective. The combination of seniors and juniors itself can be considered effective as team design that has a developmental function.

Furthermore, given the redefinition of the boundary between humans and AI discussed in Section 2.5, the focus of skills to be developed is also updated. Rather than training specific "human skills" in a fixed manner, what is required is developing the ability to continuously adapt to the shifting boundary.

#### 4.3.2 Risks If Not Achieved

If talent capable of the new engineering is not developed, advancing AI utilization at the organizational level stalls. If cognitive atrophy degrades the organization's overall critical thinking capability, reliability assurance collapses. Talent development and reliability are inseparable.

### 4.4 Organizational Acquisition of Product Envisioning Capability

#### 4.4.1 Content of the Breakthrough

What awaits beyond the resolution of development bottlenecks is a competition of envisioning capability—"what to build." Specifically, the following elements are considered:

1. Establishing the rapid hypothesis validation cycles described in Section 2.3 at the organizational level. Ensuring the conditions for rapidly withdrawing unsuccessful products is the prerequisite.
2. Redefining the form of products themselves. As Yoshiba stated, "インターフェースが全部チャットになるとか、入力デバイスが変わるとか、プロダクトの形も変わる可能性を想像すべき (We should imagine the possibility that all interfaces become chat, input devices change, and the form of products changes too)"—the ability to envision product forms that are not mere extensions of the status quo.
3. Bidirectional overlap between business and engineering. As a development of the product owner role transformation discussed by West [24], boundary dissolution progresses where engineers engage in product strategy and business-side personnel engage in development through AI.

#### 4.4.2 Risks If Not Achieved

If development accelerates but envisioning capability does not keep pace, the result is "mass production of waste." A situation where vast amounts of software are produced but none deliver value to users is not just a waste of resources—it also creates technical debt through the bloating of unmaintainable codebases. As Urushibara stated, a future may materialize where "膨大に無駄なことをやる人と、本当にちゃんと価値にフォーカスできる人とで、極端に差が出る (The gap becomes extreme between those who do a vast amount of wasteful things and those who can truly focus on value)."

## 5. Conclusion

What this report has revealed is that the most important thing for AI-driven agile toward 2030 is **not accelerating any single part of the lead time, but sequentially resolving bottlenecks across the entire feedback loop**.

As of 2026, bottlenecks in the development phase are being rapidly resolved by AI. However, bottlenecks are merely shifting to upstream (what to build) and downstream (market validation cycle). Continuing to accelerate only development in this state does not change the value of the product.

To reach an ideal future by 2030, four breakthroughs are needed:

- **Systematization and sharing of knowledge externalization** is the foundation for effectively driving AI agents.
- **Refined design of Human in the Loop and reliability assurance** ensures the quality of AI output as a systemic mechanism and transforms human intervention from "quantity" to "quality."
- **Renewal of talent development models** develops talent capable of practicing the new engineering and prevents cognitive atrophy.
- **Organizational acquisition of product envisioning capability** prepares for the essential competition that lies beyond the resolution of development bottlenecks.

These breakthroughs have independent value but also mutually reinforce each other.

The boundary between humans and AI is not fixed—it continues to shift. Rather than trying to defend specific skills as a "moat," both individuals and organizations are called upon to continuously adapt to the shifting boundary.

AI is an amplifier. What it amplifies depends on our own choices. Will it amplify exceptional knowledge and envisioning capability, or will it amplify lack of planning and inertia? The future of 2030 is determined not by the evolution of technology, but by how well we humans and our organizations can adapt.

## References
[1] Ayers, J. W., et al.: Comparing Physician and Artificial Intelligence Chatbot Responses to Patient Questions. JAMA Internal Medicine 183, no. 6 (2023)

[2] Azegami, T.: X(Twitter) Post. https://x.com/TakanoriAzegami/status/2020796425852932578 (2026)

[3] Beck, K., et al.: Manifesto for Agile Software Development. https://agilemanifesto.org/ (2001)

[4] Chakrabarty, T., et al.: Art or Artifice? Large Language Models and the False Promise of Creativity. CHI'24 (2024)

[5] Chen, J., Xu, X., Wei, H., Chen, C. and Zhao, B.: SWE-CI: Evaluating Agent Capabilities in Maintaining Codebases via Continuous Integration. arXiv:2603.03823 (2026)

[6] DeBellis, D., et al.: DORA 2025 State of AI-assisted software development report. Google. https://dora.dev/research/2025/dora-report/ (2025)

[7] Doshi, A.R. and Hauser, O. P.: Generative AI enhances individual creativity but reduces the collective diversity of novel content. Science Advances 10, no. 28 (2024)

[8] Guzik, E. E., Byrge, C. and Gilde, C.: The originality of machines: AI takes the Torrance Test. Journal of Creativity 33, no. 3 (2023)

[9] Kniberg, H.: Agile in the Age of AI. Hups Blog. https://hups.com/blog/agile-in-the-age-of-ai (2024)

[10] Lee, H.-P., et al.: The Impact of Generative AI on Critical Thinking: Self-Reported Reductions in Cognitive Effort and Confidence Effects From a Survey of Knowledge Workers. CHI'25 (2025). DOI: 10.1145/3706598.3713778

[11] Mancoridis, M., Weeks, B., Vafa, K. and Mullainathan, S.: Potemkin Understanding in Large Language Models. Proceedings of the 42nd ICML (2025)

[12] Meng, et al.: Effects of Employee–Artificial Intelligence (AI) Collaboration on Counterproductive Work Behaviors (CWBs). Behavioral Sciences 15, no. 5 (2025)

[13] National Institute of Standards and Technology: Secure Software Development, Security, and Operations (DevSecOps) Practices. NIST SP 1800-44A (2025)

[14] Pezzè, M., Abrahão, S., Penzenstadler, B., Poshyvanyk, D., Roychoudhury, A. and Yue, T.: A 2030 Roadmap for Software Engineering. ACM Trans. Softw. Eng. Methodol. 34, no. 5 (2025)

[15] Riggins, J.: Will AI replace the agile coach? LeadDev. https://leaddev.com/communication/will-ai-replace-the-agile-coach (2024)

[16] Robinson, J. B.: Futures under glass: A recipe for people who hate to predict. Futures, 22(8), 820–842 (1990)

[17] Salvi, F., et al.: On the Conversational Persuasiveness of GPT-4. Nature Human Behaviour 9, no. 8 (2025)

[18] Sharma, M., et al.: Towards Understanding Sycophancy in Language Models. ICLR 2024. arXiv:2310.13548 (2024)

[19] Shen, J. H. and Tamkin, A.: How AI Impacts Skill Formation. arXiv:2601.20245 (2026)

[20] Snowden, D. J. and Quinlan, T.: Future Backwards. Cynefin Wiki. https://cynefin.io/wiki/Future_backwards

[21] Strachan, J.W.A., et al.: Testing theory of mind in large language models and humans. Nature Human Behaviour 8, no. 7 (2024)

[22] Ullman, T.: Large Language Models Fail on Trivial Alterations to Theory-of-Mind Tasks. arXiv:2302.08399 (2023)

[23] Vaccaro, M., Almaatouq, A. and Malone, T.: When Combinations of Humans and AI Are Useful: A Systematic Review and Meta-Analysis. Nature Human Behaviour 8, no. 12, 2293–2303 (2024)

[24] West, D.: AI – A Valuable Teammate in Product Ownership. Scrum.org Blog (2025)

[25] Wischnewski, M., Krämer, N. and Müller, E.: Measuring and Understanding Trust Calibrations for Automated Systems: A Survey of the State-Of-The-Art and Future Directions. CHI'23 (2023). DOI: 10.1145/3544548.3581197

[26] Wolpers, S.: The Agile AI Manifesto. Scrum.org Blog (2025)

[27] Xie, L. and Ostrowski, E. J.: Comparing the effectiveness of LLM-Powered coaching with human coaching and GPT conversation. The Journal of Positive Psychology (2025)

[28] ULS Group: 札幌市の基幹システム標準化プロジェクトで「Devin」を活用（プレスリリース）. https://www.ulsconsulting.co.jp/news/press/2025-12-24.html (2025)

[29] Yoshiba, R.: 生成AIでスクラムによる開発はどう変わるか. https://slide.meguro.ryuzee.com/slides/127 (2025)

### Interviews

The following interviews were conducted for the preparation of this report. These interview records are published alongside this report.

- Tsuyoshi Ushio: Feb 20, 2026, Public Interview at MLSE Winter Camp 2026
  - https://github.com/mlse-jssst/ai-and-agile-future/blob/v1.1/research/v1/interview-20260220-ushio.md
- Ryutaro Yoshiba: Mar 23, 2026
  - https://github.com/mlse-jssst/ai-and-agile-future/blob/v1.1/research/v1/interview-20260323-ryuzee.md
- Shigeru Urushibara: Mar 27, 2026
  - https://github.com/mlse-jssst/ai-and-agile-future/blob/v1.1/research/v1/interview-article-20260327-urushibara.md
