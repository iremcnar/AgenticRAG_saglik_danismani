# 🏥 Sağlıkta Yapay Zeka: Agentic RAG ile Akıllı Sağlık Danışmanı

Bu proje, **Burdur Mehmet Akif Ersoy Üniversitesi** bünyesindeki **Sağlıkta Yapay Zeka** dersi uygulama çalışmaları kapsamında geliştirilmiştir. Projenin amacı, statik bir bilgi tabanı yerine internetten gerçek zamanlı araştırma yapabilen ve karmaşık sağlık sorularına kanıta dayalı yanıtlar üreten bir **Ajan tabanlı RAG (Retrieval-Augmented Generation)** sistemi geliştirmektir.

## 📌 Proje Özeti
Klasik RAG sistemleri sadece kendisine verilen belgelerle sınırlıdır. Bu projede geliştirilen **Agentic RAG**, bir LLM'in (Large Language Model) sadece cevap üretmekle kalmayıp, cevabı bulmak için hangi araçları (Search, Database vb.) kullanacağına kendisinin karar verdiği dinamik bir yapı sunar. Sistem, kullanıcıdan gelen tıbbi soruları analiz eder, gerekirse web araması yapar ve kaynak göstererek yanıt üretir.

## 🛠️ Kullanılan Teknolojiler
- **LangGraph:** Ajanın karar mekanizmasını ve döngüsel iş akışlarını yönetmek için.
- **LangChain:** LLM entegrasyonu ve araç (tool) tanımlamaları için.
- **Tavily Search API:** Tıbbi makaleler ve güncel kılavuzlar için optimize edilmiş web arama motoru.
- **OpenAI / Cohere / Groq:** Akıl yürütme (reasoning) yeteneği yüksek dil modelleri.
- **Python:** Tüm sistemin omurgası olarak.

## 🚀 Proje Uygulama Adımları

### 1. Ajan Tasarımı ve Araç Tanımlama (Tooling)
- **Tavily Tool:** Ajanın internete erişmesini sağlayan temel araçtır.
- **System Prompt:** Ajanın bir "Sağlık Danışmanı" gibi davranması, mutlaka kaynak göstermesi ve tıbbi tavsiye yerine bilgi verme amacı taşıdığını belirtmesi sağlanmıştır.



### 2. İş Akışı (Graph Workflow)
Sistem bir **StateGraph** yapısı üzerine kurulmuştur:
- **START:** Kullanıcı soruyu sorar.
- **Reasoning Node:** LLM, soruyu cevaplamak için internete bakması gerekip gerekmediğine karar verir.
- **Action/Tool Node:** Eğer gerekiyorsa Tavily Search çalıştırılır ve veriler toplanır.
- **Generation Node:** Toplanan bilgiler harmanlanarak kullanıcıya son yanıt iletilir.



### 3. ReAct Pattern (Reason + Act)
Ajan, karmaşık sorularda adım adım düşünme (*Chain of Thought*) yöntemini uygular:
1. **Düşünce:** "Kullanıcı gebelikte hipertansiyonu sordu, güncel kılavuzlara bakmalıyım."
2. **Eylem:** Tavily üzerinden arama yap.
3. **Gözlem:** Arama sonuçlarını analiz et.
4. **Yanıt:** Elde edilen verilerle kaynaklı cevap oluştur.

## 📊 Öne Çıkan Bulgular
- **Dinamik Bilgi Erişimi:** Sabit modellerin aksine, sistemin 2024 ve 2025 yılına ait en güncel tıbbi kılavuzlara ulaşabildiği doğrulanmıştır.
- **Halüsinasyon Engelleme:** Ajanın, cevabı bilmediği durumlarda uydurmak yerine arama aracını kullanarak dış kaynaklara başvurması, bilgi doğruluğunu artırmıştır.
- **Kaynak Gösterme:** Üretilen her yanıtın altına eklenen URL ve referanslar, sistemin güvenilirliğini pekiştirmiştir.

## 📂 Dosya Yapısı
- `AgenticRAG.ipynb`: LangGraph kurulumu, Ajan düğümlerinin (nodes) tanımlanması ve test senaryolarını içeren ana dosya.
- `.env`: API anahtarlarının (Tavily, OpenAI/Cohere) yönetildiği yapılandırma dosyası.

---
**⚠️ Önemli Uyarı:** Bu proje eğitim amaçlı geliştirilmiştir. Üretilen yanıtlar tıbbi tavsiye niteliği taşımaz. Sağlık sorunlarınız için mutlaka bir hekime danışınız.
