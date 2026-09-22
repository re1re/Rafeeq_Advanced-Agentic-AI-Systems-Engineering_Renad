# Rafeeq_Advanced-Agentic-AI-Systems-Engineering_Renad

<div align="center">

# 🛡️ Rafeeq Mini (رفيق)
### Production-Grade Agentic AI Architecture with Deterministic Safety & MCP Isolation

[![SDAIA Academy](https://img.shields.io/badge/SDAIA_Academy-Capstone_Project-002B49?style=for-the-badge&logo=shield)](https://github.com/SDAIAAcademy)
[![Security Baseline](https://img.shields.io/badge/Security_Suite-100%25_Passed-006d77?style=for-the-badge&logo=checkmarx)](reports/assessment_results.json)
[![Functional Suite](https://img.shields.io/badge/Functional_Suite-100%25_Passed-2a9d8f?style=for-the-badge&logo=testing-library)](reports/assessment_results.json)
[![Privacy & Tracing](https://img.shields.io/badge/Trace_Hygiene-Redacted_&_Compliant-e76f51?style=for-the-badge&logo=git)](reports/trace.jsonl)

<p align="center">
  <b>Advanced Agentic AI Systems Engineering · Capstone Implementation</b><br>
  مرجع أكاديمية سدايا على GitHub: <a href="https://github.com/SDAIAAcademy">SDAIA Academy GitHub</a>
</p>

---

</div>

## 📌 نظرة عامة (Overview)

نظام **"رفيق" (Rafeeq Mini)** هو منظومة ذكاء اصطناعي توكيلي متعددة الوكلاء (Multi-Agent System) مصممة لخدمة العملاء والعمليات اللوجستية في منصات التجارة الإلكترونية. يجمع النظام بين مرونة استدلال النماذج اللغوية الكبيرة (LLMs) والتحكم البرمجي الحتمي (Deterministic Engineering) لضمان حماية المعاملات المالية، عزل هويات العملاء، والتصدي للهجمات الموجهة.

---

## 🏛️ الرسم البياني للمسار المعماري (System Architecture)

يوضح المخطط البياني أدناه جدار الحماية وعزل البيانات بين المدخلات غير الموثوقة والخادم الخلفي الموثوق[cite: 2, 4]:

```mermaid
flowchart TD
    subgraph Untrusted_Zone ["منطقة غير موثوقة (Untrusted)"]
        User(["👤 مدخلات العميل / Customer Ticket"])
    end

    subgraph Bounded_Graph ["بيئة التشغيل المقيدة (Bounded Graph Runtime)"]
        IG["🛡️ حارس المدخلات (Input Guard)"]
        Sup{"🧠 المنسق الخفيف (Thin Supervisor)"}
        
        subgraph Specialists ["الوكلاء المتخصصون"]
            OA["📦 وكيل الطلبات (OrdersAgent)"]
            RA["💳 وكيل الاسترداد (RefundAgent)"]
        end
        
        OG["🔍 حارس المخرجات (Output Guard)"]
    end

    subgraph Trusted_Host ["الخادم المضيف الموثوق (Trusted Host)"]
        MCP["🔌 Tawseel MCP Server"]
        DB[(📁 قاعدة البيانات والطلبات orders.csv)]
        Auth["🔑 سياق الهوية الموثوق (Host Identity Context)"]
        HumanGate{"⚠️ بوابة الموافقة البشرية (> 500 SAR)"}
    end

    User -->|نص الطلب| IG
    IG -->|فحص الأمان| Sup
    Sup -->|توجيه| OA
    Sup -->|توجيه| RA
    
    OA <-->|استعلام فقط stdio| MCP
    RA <-->|طلب إجراء مالي| MCP
    
    MCP --> Auth
    MCP --> DB
    MCP --> HumanGate
    
    OA --> OG
    RA --> OG
    OG -->|الرد النهائي المنقح| User

    classDef guard fill:#e76f51,stroke:#b23b1e,stroke-width:2px,color:#fff;
    classDef agent fill:#006d77,stroke:#004950,stroke-width:2px,color:#fff;
    classDef host fill:#2a9d8f,stroke:#1d6a60,stroke-width:2px,color:#fff;
    class IG,OG guard;
    class Sup,OA,RA agent;
    class MCP,DB,Auth,HumanGate host;
