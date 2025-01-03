# Performing Incident Response

*درس انهارده هيكون مختص اكتر بالناس اللي حابه تشتغل as SOC Analyst*

## SOC Analyst

- وظيفه ال SOC Analyst او بالأخص قسم ال SOC هو خط الدفاع الاول للشركه وبيتقسمو لتلت طبقات
SOC L1 , SOC L2, SOC L3 وكل layer بيكون ليه وظيفه معينه بس كلهم بيتعاونو مع بعض عشان هدف معين
- ياعم اهدي شويه انا مفهمتش حاجه!!….انا هفهمك وظيفه ال SOC هيا مراقبه كل ال traffic اللي بيمر عبر الشبكه بتاعتي وبشوف حل هو normal ولا up normal
- خلي بالك قسم ال SOC بيكون منقسم ل SOC و Incident Response وهنشرح يعني ايه قدام
- عاوزك تكون عارف برضو اني ال SOC عامل زي فرد الامن مبينامش يعني بيكون شغال 24/7

---

## INCIDENT RESPONSE PROCESS

 **Incident response policy**

- دي البوليسي اللي فيها بيكون موجود العمليات والارشادات اللي ال IR Team هيستخدمها عشان يصد الاتاك
- لازم يكون عندي IR عشان اقدر اتعامل مع ال attacks اللي بتتعمل عليا
- قسم ال IR هو المتخصص في الدفاع عن الattack وبيكون التيم ده جوا قسم ال SOC

## مثال

- انت بتكون شغال علي الشبكه عادي وفي traffic طبيعي شغال هنا حصل Event او حدث يعني لو انا هنا بفتح تويتر او بعمل اي حاجه عبر الشبكه وبيعدي طب لو الtraffic مش طبيعي؟

![image.png](image.png)

- لو مثلا جيت افتح تويتر والمفروض اني ال firewall مانع اني حد يفتح موقع تويتر فا هنا حصل Incident حصل حاجه up normal دي ممكن تكون محاولة اختراق فا ال SOC هما اللي بيكتشفو حاجه زي دي بيروح تيم ال IR هو اللي متعامل معاها ويوقفوها وبعد صد الاتاك بيبعتو report لل Security Engineer بيشرحو فيه الاتاك حصل ازاي وامتي ومين اللي عملو ونقاط الضعف اللي ف ال firewall عشان يعدلها

![image.png](image%201.png)

### طريقة عمل الـ Incident Response Team

1. **Preparation**
- دي من اسمها اول مرحله من مراحل عمل ال IR Team ف اني هما بيجهزو الادوات والتقنيات والتاكتيكس اللي هيستخدموها في التعامل مع ال Incidents وال Attacks
1. **Identification**
- عملية تحديد وفحص تفاصيل ال Incident وبيشوفو مصدرها ايه وايه محتواها وبيحددو اذا كان هيا normal ولا Up normal
1. **Containment**
- عملية الاحتواء , ببساطه لما يحصلي attack بيبدأ ال IR يعزل الجهاز اللي حصلو الاتاك عن بقيت الاجهزه عشان ال Malware مينتشرش ف بقيت الاجهزه
- يعني مثلا لو نفترض اني قسم ال HR حصلو attack فا بيبدأ ال IR يعزل الاجهزه دي عن الشبكه بأنهم مثلا يفكو الكابلات وكدا عشان ال malware مينتشرش ويروح للاقسام التانيه
1. **Eradication**
- عملية تدمير ال Incident اللي هو خلاص بمسح بقي الحاجات اللي كانت السبب اني الاتاك دي تحصل واعيد تكوين النظام من تاني
1. **Recovery**
- بعد ما ادمر واخلص وبتاع بيكون في داتا طبعا كانت علي الجهاز ومع ال attack ممكن تكون اتمسحت او مع مرحلة ال Eradication ممكن تكون اتمسحت لأني في اوقات بضطر اعمل Format فا ال Recovery هي عملية استرجاع الداتا من خلال backup انا عامله
1. **Lessons learned**
- الدروس المستفادة , يعني لما بتحصل ال attack خلاص بيبدأ تيم ال IR يبعت report لل Sec Admin زي ما قولنا فوق ويقولو ايه الحصل عشان غالبا بيكون في misconfiguration في asset معينه او برضو لما تحصل الهجمه فا تيم ال IR بيستفاد وبيعرف طريقه جديده الهاكر بيخش منها فا بيستفادو من حاجه زي دي

![image.png](image%202.png)

✓Cyber Incident Response Team (CIRT)
✓Computer Security Incident Response Team (CSIRT)
✓Computer Emergency Response Team (CERT)

---

## INCIDENT RESPONSE PLAN

**incident response plan (IRP)**

دي عباره عن الإجراءات، وجهات الاتصال، والموارد المتاحة للمستجيبين لأنواع مختلفة من الحوادث.

- **دور فريق CSIRT**:
    
    لازم يطور **سيناريوهات** أو **بروفايلات** للحوادث الشائعة زي:
    
    - هجوم **DDoS**
    - انتشار **فيروسات/ديدان**
    - **تسريب بيانات** من مهاجم خارجي
    - **تعديل بيانات** من مهاجم داخلي
    
    ده بيساعد في تحديد الأولويات ووضع خطط العلاج.
    
- **الـ Playbook**:
    
    عبارة عن **إجراءات تشغيل قياسية (SOP)** تعتمد على البيانات، وبتساعد المحللين المبتدئين في:
    
    - اكتشاف الحوادث.
    - الاستجابة لتهديدات معينة زي:
        - هجمات **Phishing**
        - **SQL Injection** لتسريب البيانات
        - الاتصال بعناوين IP محظورة.
- **بداية الـ Playbook**:
    
    بتبدأ بتقرير **SIEM** واستعلام مصمم لاكتشاف الحادث، مع تحديد خطوات:
    
    - الاكتشاف
    - الاحتواء
    - الإزالة

---

## CYBER KILL CHAIN ATTACK FRAMEWORK

*دا نظام او مجموعة مراحل ال Attack اللي الهاكر بيمشي عليها عشان يعمل attack وبيكون ال SOC عارفها**

- بيقولك اني الاستجابه الفعاله لل Incidents بتعتمد علي Threat intelligence كويس في انو يعرف اخر الاخبار والثغرات والـ tactics , الـ techniques , الـ procedures المختلفه (TTP) عشان يكون ال IR سابق الاتاكر بخطوه

---

1. **Reconnaissance**
- دي اول عملية الهاكر بيعملها وهي مرحلة جمع المعلومات يعني بيعرف مين صاحب الشركه ايه الاقسام اللي فالشركه ايميلات الموظفين ايه التقنيات اللي الشركه شغاله بيها وهكذا
1. **Weaponization**
- بعد ما يجمع معلومات عن الشركه الهاكر بيحدد هنا السلاح او الثغره اللي هيستغلها
1. **Delivery**
- بعد ما يختار السلاح الهاكر هنا بيشوف انهي طريقه هيوصل بيها ال payload سواء عن طريق ميل او رساله او فلاشه مثلا
1. **Exploitation**
- بعد ما الهاكر يبعت ال payload وال victim يتفاعل مع الرساله او يفتح اللينك او ايا كان هنا يحصل ال Exploitation والهاكر فعليا دخل علي الجهاز
1. **Installation**
- بعد ما يحصل ال Exploitation والجهاز بقي Vulnerable خلاص الهاكر هنا بيسطب Malware يقدر يخش منو علي الجهاز زي Backdoors او Trojan عشان يقدر يخش عليه
1. **Command and control (C2 or C&C)**
- الهاكر بيتحكم في جهاز ال victim ويقدر ينزل حاجات تانيه اضافيه
1. **Actions on objectives**
- الهاكر هنا بقي بيبدأ يشتغل علي الهدف بتاعه اللي هو اصلا بيهكر الجهاز عشانه سواء بقي يسرق بيانات او يخرب حاجه معينه او يمسح داتا

![image.png](image%203.png)

---

## INCIDENT IDENTIFICATION

- **Identification**

-هنا بيتم تحديد انهي traffic يعتبر incident وكيفية التعامل معاه

- **First Responder**
- لما يتم اكتشاف حدث مشبوه، من المهم إن الشخص المناسب في **CIRT** يتم إشعاره علشان يتولى الموقف ويضع استجابة مناسبة
- الشخص ده بنسميه **First Responder**
- ده معناه إن لازم الموظفين في جميع مستويات المنظمة يتدربوا على التعرف على الحوادث الأمنية الحقيقية أو المشكوك فيها، وكمان يتعلموا إزاي يتعاملوا معاها بشكل مناسب
- **Correlation**
- الـ **SIEM** بيشغل **correlation rules** على المؤشرات المستخرجة من مصادر البيانات علشان يكتشف الأحداث اللي لازم تتراجع كحوادث محتملة
- ممكن تصفي أو تستعلم البيانات بناءً على نوع الحادث اللي تم الإبلاغ عنه
- **الCorrelation** يعني تفسير العلاقة بين البيانات الفردية علشان تشخيص الحوادث المهمة لفريق الأمان.
- قاعدة **SIEM correlation rule** هي عبارة عن تصريح بيوفق بعض الشروط
- القواعد دي بتستخدم تعبيرات منطقية زي **AND** و **OR**، وعوامل زي **==** (مطابقة)، **<** (أقل من)، **>** (أكبر من)، و **in** (يحتوي)
- **مثال على Correlation**
    - فشل دخول مستخدم واحد مش هيكون حالة تستدعي التنبيه
    - لكن فشل دخول متعدد لنفس الحساب في نفس الساعة هو الأكثر احتمالًا يحتاج تحقيق وهو اللي هيتم اكتشافه عن طريق **correlation rule**:
        - `Error.LogonFailure > 3 AND LogonFailure.User AND Duration < 1 hour`
- **استخدام Threat Intelligence في الـ SIEM**
    - بجانب الـ **correlation** بين المؤشرات اللي بتلاحظها على الشبكة، الـ **SIEM** غالبًا بيكون متصل بـ **threat intelligence feed**
    - ده معناه إن البيانات اللي بتلاحظها على الشبكة يمكن ربطها مع مؤشرات معروفة لتهديدات، زي **IP addresses** و **domain names**
    - التحليل المعتمد على **AI** بيساعد في التنبيه المتقدم والكشف عن السلوك الغريب

---

## SIEM DASHBOARDS

- ال SIEM دي النقطة المركزيه اللي بيتم تجميع فيها كل ال log بتاع اجهزة الشركه عشان ال SOC يقعد يراقب كل ال Log بتاع كل الاجهزه من خلال جهاز واحد عشان مش هيفضل يعدي علي كل جهاز يشوف ال Log يعني

---

## SIEM USED PROTOCOLS

1. Syslog
2. journalctl
3. NXLog

---

## NETWORK, OS, AND SECURITY LOG FILES

- **System and Security Logs**
1. Application
2. Security
3. System
4. Setup
5. Forwarded Events
- **Network Logs**
- **Authentication Logs**
- **Vulnerability Scan Output**
- **DNS Event Logs**
- **Web/HTTP Access Logs**

---

# INCIDENT CONTAINMENT

**Isolation-Based Containment**

- **ال Isolation** يعني فصل الجزء المتأثر عن البيئة الأكبر. زي فصل السيرفر من الشبكة بعد هجوم DoS أو تشغيل تطبيق في بيئة معزولة.
- ممكن تفصل الجهاز عن الشبكة بشكل كامل (قطع الشبكة أو تعطيل منفذ السويتش).
- لو كان في أكتر من جهاز متأثر، ممكن تعزلهم باستخدام VLANs أو جدران الحماية.
- كمان ممكن تعطل حسابات المستخدمين أو خدمات التطبيقات لو تم اكتشاف هجوم.

**Segmentation-Based Containment**

- **الSegmentation** تستخدم تقنيات الشبكة لعزل الأجهزة باستخدام VLANs، قواعد التوجيه، و ACLs.
- ممكن تستخدم **honeynet** لخداع المهاجم وخلّي الهجوم يظهر كأنه مستمر، علشان تجمع بيانات تحليلية عنه.
- التحليل العكسي للبرمجيات الخبيثة ممكن يساعد في تطوير أساليب الخداع.

**Incident Eradication and Recovery**

- بعد العزل، يجب استخدام تقنيات للحد من الهجوم والتخلص من الأدوات الخبيثة أو التغييرات غير المصرح بها.
- مرحلة الاسترداد (recovery) تهدف لاستعادة النظام ليعمل بشكل طبيعي.
- من المهم التأكد من أن نفس الهجوم لا يتكرر من نفس الثغرة أو على الأقل يتم مراقبتها.

**Eradication and Recovery Steps**

- **إعادة تكوين الأنظمة المتأثرة**: إزالة الملفات الخبيثة أو استعادة النظام من النسخ الاحتياطية.
- **مراجعة الضوابط الأمنية**: التأكد من أن النظام آمن ضد الهجمات المستقبلية.
- **إبلاغ المتضررين**: لو تم سرقة كلمات المرور، يجب نصح المتضررين بتغيير كلمات المرور.

**Firewall Configuration Changes**

- **تحليل الهجوم** يساعد في معرفة الثغرة التي استغلها المهاجم.
- بعد الهجوم، يجب تغيير إعدادات الجدران النارية لمنع نفس الهجوم.
- من المهم تطبيق **الفلترة على المداخل والمخارج** لحماية الشبكة من الهجمات.

**Guidelines for Egress Filtering**

- السماح فقط بالـ **ports** المصرح بها ومنع الوصول لأماكن غير مصرح بها.
- **حظر الوصول** إلى الـ IPs المشتبه فيها.
- تأكد من أن الأجهزة اللي ما بتحتاجش الإنترنت ما تقدرش تتصل به.

---