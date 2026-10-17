---
name: medical-auth-coverage
description: "Verificador de requisitos de autorização e cobertura para procedimentos médicos. Use for: determinar se um procedimento requer autorização prévia, quais documentos são necessários para a solicitação (como guias SADT, laudos médicos), e identificar restrições de cobertura com base em tabelas de operadoras de saúde (como DoctorClin)."
---

# Medical Authorization & Coverage Checker

This skill helps Manus systematically verify health insurance coverage and authorization requirements for medical procedures, ensuring all necessary documentation is prepared before a procedure is requested.

## When to Use

Use this skill when the user needs to know:
- If a specific procedure (e.g., bone marrow biopsy, flow cytometry) requires prior authorization
- What specific documentation must accompany an authorization request
- If a procedure is classified as High Complexity (Alta Complexidade / PAC)
- If there are DUT (Diretrizes de Utilização) restrictions for a procedure

## Workflow for Checking Coverage

When asked to check coverage for a procedure, follow this workflow:

### 1. Identify the Procedure Code (TUSS)
First, identify the exact TUSS code for the procedure. If the user provides a name, you may need to use the `medical-procedure-reference` skill to find the code.

### 2. Check the Reference Table
Check the health insurance reference table (e.g., DoctorClin reference table) for the specific code.

### 3. Extract Key Information
Extract and report the following critical fields:
- **Procedimento de Alta Complexidade (PAC)**: Yes/No. If yes, it usually requires a detailed medical justification.
- **Necessita Autorização**: Yes/No. This is the most critical piece of information.
- **Documentação Necessária**: The exact list of documents required (e.g., "Guia SADT preenchida e laudo médico com justificativa detalhada").
- **DUT**: Note any DUT numbers, as these indicate clinical criteria must be met.

## Output Format

Always present authorization information in a clear, structured format:

```markdown
### [Procedure Name] (Código: [TUSS Code])

* **Requer Autorização Prévia:** [SIM/NÃO]
* **Alta Complexidade (PAC):** [SIM/NÃO]
* **Documentação Exigida:** 
  * [Item 1, e.g., Guia SADT preenchida]
  * [Item 2, e.g., Laudo médico com justificativa detalhada]
* **Observações (DUT):** [Any DUT restrictions or special notes]
```

## Hematology Specifics

For Hematology and TMO procedures, pay special attention to:
- **Exames Genéticos/Moleculares**: Often require a specific DUT (e.g., DUT Nº 110) and detailed medical justification.
- **Painéis de Imuno-histoquímica/Citometria de fluxo**: Usually require prior authorization.
- **Quimioterapia**: Always requires authorization and often a specific chemotherapy annex/form (like the Anexo de Quimioterapia DoctorClin).
