# Annotation codebook v1.1 (frozen after calibration on 40 disjoint records, before audit coding)

You are an expert coder of scientific abstracts. For each record, read ONLY the title and abstract you are
given. Code what the abstract states, not what the paper might contain. Do not use outside knowledge
about the paper. Return exactly one JSON object per record (one line), with these keys:

{"id": "...", "relevance": "...", "functions": [...], "primary_function": "...", "mechanisms": [...], "stance": "...", "confidence": 0.0}

## 1. relevance (single label)
- CORE: the abstract substantively addresses the credibility of AI/ML systems (trust, trustworthiness,
  explainability, interpretability, transparency, accountability, reliability of model outputs) AND/OR
  bias/fairness/discrimination of AI/ML systems, in an organisational or business decision context (firms,
  markets, finance, workforce, customers, operations, management, public administration or service delivery).
- RELATED: the abstract substantively addresses AI credibility or AI bias/fairness, but not in an
  organisational or business decision context (e.g., clinical diagnosis accuracy, a generic algorithm,
  a benchmark, or purely societal or philosophical framing).
- OFF: credibility or bias of AI is not a substantive theme. For example, "bias" means a statistical
  or electronic bias only, "reliability" means engineering reliability of hardware, or the terms appear in passing.

Decision rules for relevance (added after calibration):
- "Organisational or business decision context" means that the abstract frames AI as a basis for decisions,
  management, adoption, governance or service delivery by an organisation. Clinical diagnosis, nursing care,
  classroom tutoring and individual patient or student outcomes are RELATED unless the abstract addresses
  the organisation's adoption, management, procurement, compliance or governance of the AI system.
- A general legal or ethical analysis of AI is RELATED unless it addresses obligations of organisations
  (e.g., firms' or public bodies' compliance, liability, audits).
- "Substantive" means the credibility or bias issue is an objective, a measured variable, a result or a
  main argument of the study. A single motivating sentence does not count, and such a record is OFF.
- A pure accuracy or performance study with no explicit treatment of trust, explainability, transparency,
  reliability of outputs, bias or fairness is OFF.
- Non-AI senses do not count: statistical "risk of bias" in review methodology, "discrimination" meaning
  classification or separation of samples, radio-frequency or signal "interference", and hardware
  "reliability". If such senses are the only match, code OFF.

## 2. functions (multi-label, 1-3 labels) and primary_function (one of the chosen labels)
The business or application domain where the AI is used or studied.
- FIN   finance, banking, credit, insurance, investment, fintech, fraud detection
- HR    human resources, recruitment, hiring, workforce, employees, labour
- MKT   marketing, consumers, retail, e-commerce, recommender systems for customers, advertising, tourism services
- OPS   operations, supply chain, logistics, manufacturing, Industry 4.0/5.0, maintenance, quality
- MGT   management and strategy in general, organisational decision making, corporate governance, innovation, entrepreneurship
- LAW   legal, regulation, compliance, auditing, accounting, risk management, AI governance frameworks
- PUB   public sector, government, public administration, policing, justice, public policy
- HEA   healthcare and medicine (clinical or hospital)
- EDU   education and academia
- OTH   another specific sector (energy, agriculture, transport, telecom, cybersecurity operations, media)
- GEN   no specific application domain (generic or methodological AI)

## 3. mechanisms (multi-label, 0-4 labels): how the AI model may distort or interfere with decisions
- DATA   data, sampling, representation or historical bias, label bias, proxy discrimination, unfair outcomes from training data
- OPAC   opacity, black-box models, lack of explainability or interpretability, inability to justify outputs
- DRIFT  instability, lack of robustness, distribution shift, model drift, inconsistent or unreliable outputs, uncertainty
- LOOP   feedback loops, performative or self-reinforcing effects, herding, popularity bias, strategic manipulation of inputs
- RELY   human over-reliance or under-reliance, automation bias, algorithm aversion or appreciation, trust calibration
- HALL   hallucination, fabrication or misinformation produced by generative AI or LLMs
- SIM    simulation bias: AI or synthetic data used as a stand-in for humans (LLM-simulated respondents, synthetic data, digital twins, AI as judge or evaluator) and diverging from the humans it replaces
- PRIV   privacy, security, adversarial attacks, data poisoning
Rules for mechanisms (added after calibration):
- Code a mechanism only when the abstract explicitly discusses it as a problem, a risk or the object of
  study. A method that merely uses explainability as a tool (e.g., SHAP to rank features) does not by
  itself justify OPAC. Code OPAC when opacity or the need for explanations is discussed as a problem.
- DATA is about unfair or unrepresentative outcomes or data. It does not cover statistical noise or missing values.
- SIM applies only when AI outputs or synthetic data stand in for human judgements or human data and are
  treated as if they were human (simulated survey respondents, synthetic populations or customers, LLM-as-judge
  or evaluator, human digital twins). An AI system that simply makes decisions autonomously is not SIM.
- Code at most 3 mechanisms, choosing the most prominent ones.
Return [] if the abstract names none of these.

## 4. stance (single label): the abstract's overall evaluative stance toward the credibility of AI
- OPT    AI presented as credible or beneficial; the proposed method solves the trust or bias problem; risks are minor
- CAUT   balanced: benefits are conditional on safeguards, risks and benefits are both developed
- CRIT   the emphasis is on harms, failures, distrust, discrimination or the limits of AI credibility
- NEUT   technical or descriptive with no evaluative stance (e.g., a benchmark or method description)

## 5. confidence
Your confidence in the whole record's coding, from 0.0 to 1.0.

## Rules
- Code labels in upper case exactly as listed. Do not invent labels.
- Use only the title and abstract. When in doubt between two functions, include both and pick the
  more prominent one as primary_function.
- Do not consult other coders' outputs, files other than your own items file, or any classifier.
