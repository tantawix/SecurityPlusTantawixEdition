# Implementing Secure Network Designs

# SECURE NETWORK DESIGNS

- تصميم الشبكه الامن الهدف منو حماية ال endpoints اللي هيا ال pc وال laptops عشان لو الشبكه مش امنه بشكل كافي هتكون معرضه انها تخترق
- **Typical Weaknesses include:**
1. Single Point of failure
- دي معناها اني مينفعش اعتمد علي جهاز واحد فالشبكه طب ليه ايه المشكله يعني؟ المشكله انك لما تعتمد علي جهاز ولو حصل فيه عطل او تعرض للاختراق مش هيكون ليه بديل وساعتها الشبكه هتقع يعني مثلا لو عندي راوتر واحد بس فالشبكه والراوتر ده حصل فيه عطل ووقف بالتالي حركة الشبكه كلها هتقف انما لو عندي بديل ساعتها الشبكه هتكمل شغل عادي (Fault Tolerance)
1. Lack Of Documentation And Change
- دا معناه اني ميكونش عندي خريطه توضيحيه للشبكه بحيث انا كا network admin مكونش عارف pc1 فين ومتصل ب switch وف نفس الوقت اكون موزع المهام علي الاجهزه ف الشبكه يعني مخليش جهازين يعملو نفس المهمه دا غلط
1. Overdependence On Perimeter Security
- كتير من الاداريين بيكونو مفكرين اني الاختراقات ممكن تجيلك من بره بس وميهتموش انهم يحطو firewalls داخل الشبكه ال inside دا اعتقاد خاطئ لأني وارد يحصلك اختراق من حد جوا الشبكه عادي

---

# NETWORK APPLIANCES

### Switch

- بيشتغل ف ال layer 2 في ال OSI Model وبيتعامل بال MAC

[What’s OSI Model?](https://www.notion.so/What-s-OSI-Model-148cc003b83b801a928cf7b4c51c6809?pvs=21)

- مهمة السويتش انهم يربط اجهزة الشبكه ببعض عن طريق اني بوصل كابل من الpc او ال laptop للسويتش وبيكون في بورتات بوصل الكابل ده فيه
- طريقة نقل السويتش للبيانات بين الاجهزه اللي مربوطه من خلاله بتكون عن طريق ال MAC Address
- بيكون السويتس فيه حاجه اسمها MAC Table بيكون متخزن فيها ال port وال mac بتاع كل جهاز متوصل بيه بحيث لو جهاز عاوز يتواصل مع جهاز تاني يعرفو ويشوف هو علي Port كام ويبعتلو الحاجه
- ال VLAN ده ميزه بتكون فالسويتش بتقدر تفصلي جهازين او اكتر مع بعض لوحدهم كدا

![image.png](image.png)

### Wireless Access Point (WAP)

- بيشتغل ف ال layer 2 في ال OSI Model وبيتعامل بال MAC زي ال switch
- الأكسس بوينت زيو زي ال switch بس الفرق اني ال access point ممكن الاجهزه تتوصل من غير كابلات wireless يعني بالواي فاي علاطول

### Router

- بيشتغل ف ال layer 3 في ال OSI Mode وبيتعامل بال IP
- مهمة الراوتر انو يوجه ال Packets اللي جياله
- بيربط بين الشبكات وبعضها
- بيكون ليه Routing Table

### Firewall

- بيشتغل ف ال layer 3 في ال OSI Mode او اعلي
- الجدار الناري اللي بيحدد من يخرج ومين يدخل
- الفايروال بيكون اعدادات default اني اي حد من داخل الشبكه inside ينفع يأكسس علي النت عادي انما ال outside مينفعش يدخل لل Inside جوا
- بيكون فيه List اسمها Access Control List فيها مجموعه من القواعد اللي بتحدد شروط دخول ال packet او لأ
- ممكن ال admin يعدل عليه عادي وي customize الاعدادات

### Load balancer

- بيشتغل ف ال layer 4 في ال OSI Mode او اعلي
- بص يسطا , دا جهاز المفروض لما تيجي تفتح اي ويب سايت ويحصل ضغط عليه و ريكويستات كتير الموقع بيقع او لما بيحصل هجمات DOS , DDOS Attacks ايه فكرة الاتاك دي اصلا؟ اني الهاكر بيبعت وريكويستات كتير للموقع فا بيقع طب ايه رأيك اننا نعمل كذا سيرفر للموقع ويكونو ف اماكن مختلفه بعيده عن بعض ولما مثلا سيرفر يحصل عليه ريكويستات بعدد معين ال Load balancer يحولو لسيرفر ساعتها هنا يقدر يوزع الطلبات فا مش هيحصل ضغط عالسيرفر ويقع

![image.png](image%201.png)

---

# Routing & Switching Protocol

### **يعني إيه وظيفة الـ Forwarding؟**

دي ببساطة العملية اللي البيانات (Packets) بتتنقل فيها بين الأجهزة جوه الشبكة، وبتتم على مستويين مختلفين:

1. **Layer 2 (Data Link Layer).**
2. **Layer 3 (Network Layer).**

---

### **1. Layer 2 Forwarding (الطبقة الثانية):**

- هنا العملية بتحصل بين الأجهزة اللي موجودة على نفس الشبكة المحلية (Local Network Segment).
- الشبكة المحلية دي بنسميها **Broadcast Domain**، وده يعني إن أي رسالة "Broadcast" بتتبعت بتوصل لكل الأجهزة الموجودة في نفس النطاق.
- **أمثلة على Broadcast Domain:**
    - لو عندك **Switch غير مُدار (Unmanaged Switch)**، كل الأجهزة المتوصلة عليه بتكون في نفس الـ Broadcast Domain.
    - لو عندك **Switch مُدار (Managed Switch)** مع إعدادات VLAN، تقدر تقسم الشبكة دي لأكتر من Broadcast Domain.
- في الطبقة دي، كل جهاز بيتعرف عن طريق عنوانه الـ **MAC Address** (Media Access Control).
    - **MAC Address** هو رقم مميز بيتكون من 48 بت (6 أزواج من الأرقام والرموز المكتوبة بالنظام الست عشري).
    - مثال: **00-15-5D-F4-83-48.**

---

### **2. Layer 3 Forwarding (الطبقة الثالثة):**

- هنا بننتقل للـ **Routing**، وده بيحصل بين شبكات منطقية (Logical Networks) وشبكات فعلية (Physical Networks).
- لو عندك شبكة واحدة ومقسّمها لمجموعة Broadcast Domains صغيرة، بنسميها **Subnetting** (تقسيم الشبكة).
- لما نوصل أكتر من شبكة ببعض باستخدام **Routers**، بنكون حاجة اسمها **Internetwork** (شبكة بينية).
- في الطبقة دي، كل جهاز بيتعرف عن طريق عنوانه الـ **IP Address**، وده بيحدد الجهاز في الشبكة العالمية أو المحلية.

### **مثال عملي بسيط:**

- لو عندك جهازين متوصلين على نفس الـ Switch ومشغلين عليه لعبة، البيانات بينهم هتمشي على **Layer 2** باستخدام الـ MAC Address.
- لو جهازك عاوز يفتح موقع على الإنترنت، هنا البيانات هتحتاج تعدي على الراوتر، وده بيشتغل على **Layer 3** باستخدام الـ IP Address.

![image.png](image%202.png)

---

### 3.  Address Resolution Protocol (ARP)

- البروتوكول ده بستخدمو لما مكونش عارف ال MAC بتاعه جهاز معين معايا عالشبكه وعاوز اعرفو طب ايه اللي بيحصل؟
- جهازي يبيكون عارف ip الجهاز اللي عاوز يعرف ال MAC بتاعه بيروح باعت ARP لكل اجهزة الشبكه فا الجهاز صاحب ال ip هو بس اللي بيرد وبيقولو اتفضل دا ال MAC بتاعي ياعم
- طب هو ممكن حد تاني يرد غير اللي ال ip اللي انا حاطه؟ اه , ودا نوع من الهجمات اسمه ARP Spoofing

---

### Internet Protocol (IP)

- بيكون في IPv4 ودا بيكون 32 bit ومتكون من اربع مقاطع او اربعه octet وبنظام ال decimal زي مثلا 172.16.1.101
- وفي نوع تاني IPv6 ودا بيكون 128 bit ومتكون 6 octet وبيكون بال hexadecimal 2001:db8::abc:0:def0:1234

---

# NETWORK TOPOLOGY AND ZONES

- Topology ⇒ يعني دي الشكل التوضيحي او الرسمه بتاعت اي حاجه مش شرط الشبكه
- وبيكون في نوعين لل topology واحد logical وواحد physical

## Zones

### **إيه هو مفهوم الـ Zone في الشبكات؟**

- **الZone** يعني منطقة في الشبكة كل الأجهزة اللي فيها بتشارك نفس إعدادات الحماية.
- كل الأجهزة اللي موجودة في نفس الـ Zone بيبقى ليها نفس مستوى الحماية ونفس السياسات الأمنية.
- بمعنى تاني، المنطقة دي بتبقى كأنها مجموعة من الأجهزة اللي شغالة تحت نفس القواعد الأمنية.

---

### **إيه اللي بيحصل بين الـ Zones؟**

- لما البيانات تتحرك بين الـ Zones المختلفة، لازم يتم التحكم فيها كويس باستخدام جهاز أمني زي **Firewall**.
- الفايروال بيعمل حاجتين:
    1. بيحدد مين يقدر يدخل ويخرج بين الـ Zones.
    2. بيحمي الشبكة من أي تهديدات أو هجمات.

---

### **أنواع ال Zones:**

1. **Intranet / Trusted Zone (منطقة موثوقة):**
    - ودا جزء الشبكه اللي بيكون اشخاص موثوقين زي الموظفين بتوعي والاقسام اللي جوا الشركه بكل الاجهزه وال assets
2. **Extranet / Untrusted Zone (منطقة غير موثوقة):**
    - ودا بيكون الجزء الخارجي اللي هو الانترنت يعني
3. **DMZ (De-Militarized Zone - المنطقة العازلة):**
    - ودا بقي جزء بيكون مشترك بين المستخدمين اللي جايين من بره عن طريق الانترنت والموظفين فالشبكه بيكونو ف منطقه بين الشبكتين بحيث اني الحاجات اللي جوا بيستخدمها المستخدمين العاديين والموظفين برضو
    
    ![image.png](image%203.png)
    

---

# Implement Secure Switching and Routing

## Man-in-the-Middle/On-Path Attacks

- دي اتاك باينه من اسمها الرجل في المنتصف هنا الاتاكر لو عرف انو يأكسس علي الشبكه هيقدر يشوف اي traffic بين اي جهازين عالشبكه وممكن انو ينتحل شخصيه اي جهاز او يوجه جهاز معين لحاجه تانيه خالص بدل ما يروح للوجهه اللي رايحلها

![image.png](image%204.png)

## MAC Cloning

- تخيل معايا كدا لو الاتاكر عرف انو يدخل علي الشبكه ولقي في جهازين بيتواصلو مع بعض راح ماسك جهاز من الاتنين دول وعرف ال MAC وراح عامل نفس ال  MAC بتاعه بس وهمي هيروح الجهاز اللي بيتواصل مع الجهاز الاولاني يفكر انو هو ده الجهاز اللي يتواصل معاه ويبعتلو البيانات عادي طب ليه الجهاز مبعتش للأولاني لأني الاجهزه بتعترف بالعنوان الاحدث يعني الجهاز هيلاقي نفس ال MAC لجهازين هيروح مختار او يبعت لجهاز الهاكر لأنه واخد ال MAC بتاعه جديد وهو اصلا منتحل شخصيتك مش انت

![image.png](image%205.png)

## MAC Flooding

- هنا الاتاكر لو معاكو علي نفس ال switch وفي جهازين بيتواصلو مع بعض ممكن الاتاكر يبعت طلبات كتير علي نفس البورت اللي بيتواصلو منو ب ماكات ادرس وهميه وكتير فا اللي بيحصل اني ال MAC Table بتاع السويتش يتملي وطبعا هو ليه limit عشان بيكون جاي بذاكره معينه فا لما بيتملي كدا ال MAC بيتحول ل HUB طب ايه المشكله انو يشتغل كا HUB؟ لا طبعا مشكله كبيره اوي لأني اصلا من العيوب بتاعت ال HUB انو لو في جهازين بيتواصلو مع بعض الرساله بتروح لكل الاجهزه اللي ف الشبكه يعني لو محمد بيتكلم مع احمد ابراهيم اللي معاها علي نفس الشبكه هتوصلو الرساله عادي

![image.png](image%206.png)

## ROUTE SECURITY

- هنا نوع هجمه الاتاكر بيقدر يغير ف ال Routing Table بتاع الراوتر ويوديه لوجهه تانيه غير اللي هو رايح ليها

![image.png](image%207.png)

---

# WIRELESS NETWORK INSTALLATION

- طبعا زي ما احنا عارفين اني شركه دلوقتي او مؤسسه سواء مستشفي او جامعه او ما شابه بتعتمد علي الأكسس بوينت مع السويتشات برضو
- كل أكسس بوينت بيكون ليه MAC Addess خاص بيه جاي معاه جهاز ودا بنسميه basic services set identifier BSSID
- اما اسم الشبكه بيكون SSID ودا انا اللي بسميه هو بيكون جاي باسم by default بس انا ممكن اغير اسميه زي ما انا عايز
- ال wireless networks بتكون جايه 2.4 GHz او 5 GHz
- كل radio band بيبث علي channel معينه مينفعش حد يبث عليها غيره عامله زي محطات الراديو يعني لو محطة الاخبار بثت ف نفس التشانل بتاعت القران هيحصل تشويش ومش هتشتغل
- طيب لو انا مثلا ف جامعه وطبعا الجامعه بتكون كبيره جدا عاوزين نغطي كل الجامعات بالأكسس بوينت طب هنعمل ده ازاي؟ هنحط ف كل دور أكسس بوينت صح كدا بس تخيل معايا الجامعه كام دور وفيه كام أكسس هيبقو كتير لو ال network admin حب يخش بقي يظبط الاعدادات بتاعتهم هيخش علي واحد واحد؟ لأ طبعا بيكون في جهاز اسمه Wireless Controller ودا بيتوصل فيه كل الأكسس بوينت اللي عندي وهو بيتحكم فيهم كلهم بحيث انا لو عاوز اعمل لكل الأكسسات كلمة سر معينه هروح داخل علي ال Wireless Controller وهو هيتحكم ف كل الأكسسات

---

## ROGUE ACCESS POINTS AND EVIL TWINS

- ودا نوع من الهجمات اللي بيستهدف الشبكات اللاسلكيه اللي هيا الواي فاي يعني
- طبعا انا لو عندي أكسس معين وعاوز اخترقه اعمل ايه مثلا الأكسس ده اسمه auc@edu وعاوز اخترقه فا انا ممكن اجيب أكسس بوينت تاني واظبطه انو يكون بنفس الاسم بس يكون مفتوح
- انا بقي دلوقتي لو طالب وحابب اتصل بالواي فاي هلاقي في شبكتين بنفس الاسم بس واحده مقفوله وواحده تانيه مفتوحه هروح طبعا داخل عالمفتوحه وكدا كدا الموبايل بيتصل تلقائيا بالمفتوحه بمجرد انك بتفتح الواي فاي علي الموبايل
- ساعتها كدا انا اتصلت بشبكه نفس الاسم بس دي malicious عشان كدا بنسميها الهجمه دي التوأم الشرير Evil Twins
- ممكن بقي الهاكر يعمل هجمات علي الطلاب اللي اتصلو بالواي فاي زي MITM او يزرع Backdoor فالشبكه نفسها

## JAMMING ATTACKS

- دا نوع من الهجمات اللي بيعطلي الواي فاي ويغرقو ويوقفو عن الخدمه
- لو تفتكر فوق قولتلك لو في اكسس بث علي نفس تشانل اكسس تاني هيشوشو علي بعض
- دي بقي فكرة الأتاك هتجيب اكسس وتخليه يبث علي نفس تشانل اكسس الفيكتيم وساعتها هيحصل تشويش علي الشبكه وهتتعطل

---

# Implement Load Balancers

### **هجمات الحرمان من الخدمة الموزعة (DDoS):**

- **الDDoS Attack** هو نوع من الهجمات اللي هدفه **تعطيل المواقع** أو **البوابات** عن العمل باستخدام **عدد كبير من الأجهزة** في نفس الوقت.
- يعني الهجوم مش بييجي من جهاز واحد، لكن من **أجهزة كتير** (أو "بوتات") في وقت واحد، ودي الأجهزة بتكون **مخترقة** ومتحكم فيها عن طريق المهاجم.

---

### **إزاي بيشتغل الهجوم؟**

- المهاجم بيخترق أجهزة مختلفة (ممكن مئات أو آلاف أو حتى ملايين الأجهزة)، وبعد كده **بيجمعهم في شبكة** اسمها **Botnet** (شبكة بوتات).
- الشبكة دي بيستخدمها المهاجم عشان يرسل **طلبات وهمية** لزيادة الضغط على الموقع أو السيرفر، لدرجة إنه يقفل الشبكة أو الموقع ويمنع الأجهزة **الشرعية** من الوصول.

---

### **كيفية التخفيف من هجمات DDoS:**

- **مراقبة المرور:**
    
    لو لاحظت زيادات مفاجئة في حركة البيانات من غير سبب واضح، ممكن يكون ده هجوم DDoS.
    
- **الخدمات عالية التوافر (High Availability Services):**
    
    أهم حاجة لمواجهة هجمات DDoS هي توفير **خدمات متوازنة** بحيث لو واحد من السيرفرات وقع، السيرفرات التانية تكمل شغلها بدون ما يحصل توقف للخدمة.
    
- **الجدران النارية القوية (Stateful Firewalls):**
    
    بعض الجدران النارية المتطورة ممكن تكتشف هجوم DDoS وتحظر المصدر بشكل تلقائي.
    
    لكن في أغلب الأحيان، المهاجمين بيخادعوا النظام عن طريق **تغيير العناوين** (Spoofing) أو الهجوم من خلال **البوتات**، مما يجعل من الصعب تحديد المصدر.
    

---

### **التوازن بين الأحمال (Load Balancing):**

- الـ **Load Balancer** هو جهاز أو نظام بيعمل على **توزيع الطلبات** بين مجموعة من السيرفرات عشان متكونش فيه سيرفر واحد بيتحمل كل الحمل.
- ده بيقلل الضغط على السيرفرات وبيساعد في **مواجهة هجمات DDoS**.

---

### **أنواع الـ Load Balancers:**

1. **Layer 4 Load Balancer:**
    
    بيقرر توزيع الحمل بناءً على **عنوان الـ IP** و**منفذ TCP/UDP**، وده بيكون شغال في الطبقة الرابعة في نموذج OSI.
    
2. **Layer 7 Load Balancer (Content Switch):**
    
    ده بيقدر يوزع الحمل بناءً على **بيانات التطبيق** نفسها زي **طلبات URL معينة** أو **أنواع البيانات** (زي الفيديو أو الصوت)، وده بيحتاج **منطق معقد** لكن الأجهزة الحديثة قادرة تدير ده بسهولة.
    

---

### **أمثلة على استخدام الـ Load Balancer:**

- لو عندك سيرفرات ويب، سيرفرات بريد إلكتروني، أو سيرفرات **مؤتمرات الفيديو**، فممكن تستخدم **Load Balancer** علشان توزع الطلبات بين السيرفرات وتضمن **استمرارية الخدمة**.
- في حالة تعطل سيرفر، الـ Load Balancer يوجه الطلبات للسيرفرات التانية اللي شغالة، فالمستخدمين ما يحسوش بأي تأخير أو توقف في الخدمة.

---