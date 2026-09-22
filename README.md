<div align="center">

# 🛡️ Rafeeq Mini (رفيق)
### Advanced Agentic AI Systems Engineering · Capstone Project
**Eng. Renad**

[![SDAIA Academy](https://img.shields.io/badge/SDAIA_Academy-Capstone_Project-002B49?style=for-the-badge&logo=shield)](https://github.com/SDAIAAcademy)
[![Security Suite](https://img.shields.io/badge/Security_Suite-11%2F11_Passed_(100%25)-006d77?style=for-the-badge&logo=checkmarx)](reports/assessment_results.json)
[![Functional Suite](https://img.shields.io/badge/Functional_Suite-100%25_Passed-2a9d8f?style=for-the-badge&logo=testing-library)](reports/assessment_results.json)
[![Privacy & Tracing](https://img.shields.io/badge/Trace_Hygiene-Redacted_&_Compliant-e76f51?style=for-the-badge&logo=git)](reports/trace.jsonl)

<p align="center">
  <b>Deterministic Safety Guardrails · Bounded Execution · MCP Tool Isolation</b><br>
  مرجع أكاديمية سدايا على GitHub: <a href="https://github.com/SDAIAAcademy">SDAIA Academy GitHub</a>
</p>

---

</div>

## 📌 نظرة عامة (Overview)

نظام **"رفيق" (Rafeeq Mini)** هو منظومة ذكاء اصطناعي توكيلي متعددة الوكلاء (Multi-Agent System) مصممة لمحاكاة خدمة العملاء والعمليات اللوجستية في منصات التجارة الإلكترونية. يجمع النظام بين مرونة استدلال النماذج اللغوية (LLMs) والتحكم البرمجي الحتمي الصارم (Deterministic Engineering) لضمان أمان المعاملات المالية، عزل هويات العملاء، والتصدي للهجمات الموجهة وتصعيد الصلاحيات.

---

## 🏛️ الرسم البياني للمسار المعماري (System Architecture)

يوضح المخطط البياني أدناه جدار الحماية وعزل البيانات بين المدخلات غير الموثوقة والخادم الخلفي الموثوق:

```mermaid
flowchart TD
    subgraph Untrusted_Zone ["منطقة غير موثوقة (Untrusted)"]
        User(["👤 Customer Ticket / مدخلات العميل"])
    end

    subgraph Bounded_Graph ["بيئة التشغيل المقيدة (Bounded Graph Runtime)"]
        IG["🛡️ Input Guard / حارس المدخلات"]
        Sup{"🧠 Thin Supervisor / المنسق"}
        
        subgraph Specialists ["الوكلاء المتخصصون"]
            OA["📦 OrdersAgent / وكيل الطلبات"]
            RA["💳 RefundAgent / وكيل الاسترداد"]
        end
        
        OG["🔍 Output Guard / حارس المخرجات"]
    end

    subgraph Trusted_Host ["الخادم المضيف الموثوق (Trusted Host)"]
        MCP["🔌 Tawseel MCP Server"]
        DB[(📁 Orders Database / orders.csv)]
        Auth["🔑 Host Identity Context / سياق الهوية"]
        HumanGate{"⚠️ Human-in-the-Loop (> 500 SAR)"}
    end

    User -->|Ticket Prompt| IG
    IG -->|Sanitized State| Sup
    Sup -->|Route Decision| OA
    Sup -->|Route Decision| RA
    
    OA <-->|Read-only stdio| MCP
    RA <-->|Write Request| MCP
    
    MCP --> Auth
    MCP --> DB
    MCP --> HumanGate
    
    OA --> OG
    RA --> OG
    OG -->|Audited Reply| User

    classDef guard fill:#e76f51,stroke:#b23b1e,stroke-width:2px,color:#fff;
    classDef agent fill:#006d77,stroke:#004950,stroke-width:2px,color:#fff;
    classDef host fill:#2a9d8f,stroke:#1d6a60,stroke-width:2px,color:#fff;
    class IG,OG guard;
    class Sup,OA,RA agent;
    class MCP,DB,Auth,HumanGate host;
├── .github/workflows/          # خط عمل التحقق الآلي المستمر
├── data/public/                # بيانات التقييم وقاعدة بيانات الطلبات
├── mcp_server/                 # خادم بروتوكول سياق النموذج (Tawseel MCP Server)
├── notebooks/
│   └── Rafeeq_Mini_Capstone.ipynb  # الدفتر البرمجي المعتمد للمشروع
├── reports/
│   ├── checkpoints/            # تقارير البوابات اليومية ونقاط التحقق
│   ├── assessment_results.json # التقييم الشامل المعتمد
│   ├── monitoring_dashboard.png# رسم بياني لمؤشرات الأداء
│   ├── submission_manifest.json# بيان سلامة الحزمة المعتمدة
│   └── trace.jsonl             # سجلات التتبع الآمنة والمنقحة
├── scripts/                    # سكربتات بوابات الجودة والتصدير الآلي
├── src/rafeeq/                 # محرك النظام، الحراس، ومنطق التدفق
├── LEARNING_PROGRESS.md        # سجل تقدم المتدرب وتمارين TODOs
└── README.md                   # التوثيق العام للمشروع
# 1. التحقق من سلامة التصدير المسبق وخلو المشروع من الأسرار
python scripts/export_safety_check.py

# 2. تشغيل فحص التسليم الشامل ومطابقة عقود التقييم
python scripts/validate_submission.py
