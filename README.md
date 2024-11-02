<div align=center>
       <img src="https://github.com/bitspaceorg/.github/assets/119417646/577c8581-499e-4cbb-a2f8-e78c643204bc" width="150" alt="Logo"/>
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
       <img src="https://github.com/user-attachments/assets/359035d0-6a5b-403a-ac6a-35c82db8c5b1" width="120" alt="Logo" />
  <h1>Innovation Challenge October 2024</h1>
  <img src="https://img.shields.io/badge/:bitspace-%23121011?style=for-the-badge&logoColor=%23ffffff&color=%23000000">
  <img src="https://img.shields.io/badge/Genspark-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black">
  <img src="https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=microsoftazure&logoColor=white">
  <img src="https://img.shields.io/badge/Microsoft-0078D4?style=for-the-badge&logo=microsoft&logoColor=white">
  <h1>TUSK: Trusted Utility for Statutory Knowledge </h1>
        <a href="https://1drv.ms/p/c/b7bb6097c40f3e7e/Ea7C60D-E_VIlNlTJegWmSwBJTELx5ADzkCUVHgMshmw1A?e=YCCZIl&nav=eyJzSWQiOjI2MSwiY0lkIjowfQ"> <img src="https://github.com/user-attachments/assets/73d36b52-0529-40b4-b008-012eeca5df05" width=30 />
 </a>
  &nbsp;&nbsp;&nbsp;
<a href="https://youtu.be/oX6uLK7w9MQ">
       <img src="https://github.com/user-attachments/assets/bdbba9bb-e860-4eba-890f-268abdc81730" width=30 />
</a>
  &nbsp;&nbsp;&nbsp;
<a href="http://tusk.bitspace.org.in/">
       <img src="https://github.com/user-attachments/assets/2676cd53-a2f7-4c37-abc4-1127f00fba86" width=30 />
</a>
</div>


TUSK is an innovative legal tech solution developed to streamline the compliance verification process for corporate legal documents. By leveraging the power of Large Language Models (LLMs) and advanced Retrieval-Augmented Generation (RAG) techniques, TUSK ensures that legal documentation strictly adheres to all applicable laws, rules, and regulations. With a core focus on accuracy, efficiency, and trust, TUSK is positioned as an essential tool for companies navigating complex regulatory landscapes.

# Table of Contents

1. [**Working**](#working)
   - [**Knowledge Base Creation**](#knowledge-base-creation)
   - [**RAG-Based Document Validation**](#rag-based-document-validation)
2. [**Use Case**](#use-case)
3. [**Technologies Used**](#technologies-used)
4. [**Azure**](#azure)
5. [**Architecture**](#architecture)
   - [**Frontend**](#frontend)
   - [**Backend**](#backend)
6. [**Proposal**](#proposal)
7. [**Team**](#team)
8. [**Contribution**](#contribution)

# Working

The primary goal of our project is to validate legal and regulatory compliance of documents against an established set of rules and laws. The project workflow can be divided into two main sections: **Knowledge Base Creation** and **RAG-Based Document Validation**. Here’s a detailed breakdown of each component:

### Knowledge Base Creation

To verify compliance, we first need a robust **Knowledge Base** containing all relevant rules, laws, and regulations.

1. **Input Documents**: Users provide documents that contain these rules and laws. The documents can either be in plain text format or scanned copies.
   
2. **Document Upload**: Users upload these documents via a React-based frontend interface. Upon submission, each document is securely stored in an **Azure Storage Account**.

3. **Text Extraction**: Azure’s **Document Intelligence** service is then invoked to extract text from the uploaded documents. This service supports text recognition from both typed and scanned documents, ensuring comprehensive data extraction.

4. **Ingestion into Knowledge Base**: After text extraction, users have the option to ingest this document into the Knowledge Base. 
   - **Embedding Creation**: The extracted text is converted into vector embeddings using the **Azure OpenAI model “text-embedding-3-large”**.
   - **Storage in Vector Database**: The resulting embeddings are stored in an **Azure Cognitive Search** vector store, creating a structured and searchable repository of compliance rules and regulations.

The knowledge base built through this process serves as the foundation for document validation in the next phase.

### RAG-Based Document Validation

![image](https://github.com/user-attachments/assets/c3280513-d8d6-4d8f-97ea-9601cbf955b1)

To validate external documents against the Knowledge Base, we employ a **Retrieval-Augmented Generation (RAG)** approach, ensuring a high level of accuracy and contextual understanding.

1. **Document Upload for Validation**: On a separate interface, users upload the document intended for compliance validation. Similar to the Knowledge Base setup, this document is stored in the Azure Storage Account and processed through **Azure Document Intelligence** for text extraction.

2. **Document Segmentation**: The extracted content is divided into manageable sections, enhancing analysis granularity.

3. **RAG Chain Execution**:

   <img src="https://github.com/user-attachments/assets/b7defb3b-1d1c-4009-a8af-016bb6d44af1" width="300" />

   - **Prompt Construction**: Using LangChain, we create a custom prompt template tailored for each section. The prompt contains:
      - **The document segment to be evaluated**.
      - **Contextual information** retrieved from the Knowledge Base by performing a vector search using **Azure Cognitive Search**.
      - **Previously validated content and its results**, if applicable, to strengthen the model’s decision-making.
   - **LLM Processing**: Each prompt is sent to the **Mistral 3B** language model, which evaluates the content for compliance based on the context provided. This method is called **Query Decomposition**, where each part of the document is processed separately and sequentially to ensure a thorough review.

5. **Result Aggregation and Storage**: The model’s responses for each segment are stored as individual records, capturing both the compliance outcome (legal or not) and the reasoning.

6. **Frontend Display**: The final results are presented to the user in the frontend, showing the compliance status of each document section, along with the reasons for the determination.

# Use Case

**TUSK** provides a powerful, AI-driven compliance solution designed for organizations that handle a high volume of legally sensitive or regulated documents. By ensuring documents adhere to all relevant rules, regulations, and standards, TUSK mitigates legal risks and boosts operational efficiency. Here are some practical use cases for TUSK:

1. **Corporate Compliance Checks**  
   Companies must frequently review internal documents, contracts, and policies to comply with ever-evolving legal standards. TUSK simplifies this process by automating compliance checks, enabling legal teams to validate documents efficiently and with a high degree of accuracy.

2. **Regulatory Audits**  
   Organizations in heavily regulated industries (e.g., finance, healthcare, and telecommunications) face frequent audits to ensure compliance with specific regulations. TUSK allows these companies to proactively assess documents and flag potential areas of non-compliance, ensuring they meet audit standards with ease.

3. **Contractual Agreements**  
   TUSK can assist in validating contracts, purchase agreements, or service level agreements (SLAs) by comparing each document’s clauses against regulatory standards. This reduces the risk of signing agreements that may later result in legal liabilities.

4. **Document Standardization Across Subsidiaries**  
   Large organizations with multiple subsidiaries often need to ensure consistency in compliance documents across all branches. TUSK provides a centralized platform to verify that each subsidiary's documents align with company-wide regulatory standards and best practices.

5. **Mergers and Acquisitions (M&A) Due Diligence**  
   In M&A activities, organizations conduct due diligence to evaluate the legal standing and compliance of potential acquisitions. TUSK can streamline the evaluation process by analyzing the target company’s documents for adherence to regulatory standards, reducing legal and operational risks.

6. **Insurance Claims and Policy Verification**  
   Insurance companies must often verify the compliance of claims documents and policies with industry regulations. TUSK helps insurance firms automate these checks, ensuring policies meet legal standards and claims are accurately assessed against regulations.

# Technologies Used

1. **Azure Cloud Services**  
   Azure provides the foundation for TUSK’s infrastructure, offering secure storage, text extraction, and scalable hosting. This enables seamless integration, centralized management, and efficient handling of data and AI functionalities.

2. **Models**
   - **Text-Embedding-3-Large**: Used to generate embeddings for each document ingested into the Knowledge Base, enabling efficient and contextually aware search.
   - **Mistral 3B**: Powers the document validation process through Retrieval-Augmented Generation (RAG), delivering precise analysis based on contextual legal standards.

3. **LangChain**
   - LangChain enables the RAG chain and dynamic prompt construction, integrating document sections, contextual knowledge from the Knowledge Base, and previous validation results for nuanced compliance checks.

4. **React (Frontend)**
   - React is used to build the frontend interface, allowing users to upload documents, manage the Knowledge Base, and view validation results.

5. **Flask (Backend)**
   - Flask serves as the backend framework, managing API endpoints, processing logic, and integration with Azure services for efficient handling of document processing and validation tasks.

6. **Azure SDK for Python**
   - The Azure SDK allows seamless interaction between Flask and Azure services, enabling smooth data flow and integration across the platform.

7. **Python**
   - Python powers the backend logic and supports integrations with LangChain, Azure SDK, and other modules for document processing and compliance analysis.


# Azure

1. **Azure Storage Account**  
   - Stores both Knowledge Base documents and documents uploaded for compliance validation. This service ensures secure and scalable storage for all document types, including scanned copies and extracted text.

2. **Azure Document Intelligence**  
   - Extracts text from uploaded documents, supporting both typed and scanned formats. This service provides accurate data extraction, forming the basis for embedding creation and compliance validation.

3. **Azure AI Search**  
   - Serves as the vector store, housing document embeddings generated for the Knowledge Base. This service enables fast, contextually relevant retrieval, allowing the RAG process to locate applicable regulations and standards for document validation.

4. **Azure OpenAI Labs**  
   - Provides access to the embedding model **Text-Embedding-3-Large**, used to convert Knowledge Base content into vector embeddings. These embeddings enhance the searchability and contextual accuracy of compliance checks within Azure AI Search.

5. **Azure ML Studio**  
   - Hosts the **Mistral 3B** model, used to analyze document content and validate compliance using Retrieval-Augmented Generation (RAG). This service supports robust and scalable deployment of advanced models.

6. **Azure Container Apps**  
   - Hosts and scales the backend Flask application, handling API requests and integrating processing logic. Azure Container Apps ensures that the backend remains responsive and adaptable to fluctuating demand.

7. **Azure SDK for Python**  
   - Facilitates seamless integration between Flask and Azure services, streamlining data management, storage, and retrieval processes throughout the project.

# Architecture

![arch](https://github.com/user-attachments/assets/259e488a-f199-46b9-9c52-1d10830af1ff)

# Frontend

1. **Document Upload Interface**  
   - Users can upload documents either to add to the Knowledge Base or to validate against existing regulations. The interface supports multiple file types, including both plain text and scanned documents, and each file is securely stored in the Azure Storage Account.

2. **Knowledge Base Management**  
   - The Knowledge Base section allows users to review, edit, or delete previously uploaded compliance documents. This section gives users control over the repository of rules and regulations that underpin the compliance validation process.

3. **Compliance Validation Results**  
   - For documents uploaded to be validated, the frontend displays compliance results in a clear format. Each document section is marked as compliant or non-compliant, along with a summary of the reasoning. This allows users to view detailed feedback for each segment of the document, enhancing usability and transparency.

4. **Responsive and User-Friendly Design**  
   - The React frontend is designed to be responsive and easy to navigate, supporting a seamless experience across devices and providing straightforward access to all key features.

# Backend

The backend of TUSK is developed with **Flask** and integrated with various Azure services via the **Azure SDK for Python**. The backend manages API endpoints, document processing, and the entire RAG workflow. Key functions include:

1. **API Endpoints**  
   - RESTful APIs are used to connect the frontend with backend processes, such as document uploads, retrieval of compliance results, and management of the Knowledge Base. The endpoints are secured to protect data integrity and user privacy.

2. **Document Processing Workflow**  
   - The backend orchestrates the document processing pipeline, including storage in Azure, text extraction through Azure Document Intelligence, and embedding generation using Azure OpenAI Labs. Processed documents are indexed in the Azure AI Search vector store for efficient retrieval.

3. **RAG (Retrieval-Augmented Generation) Chain**  
   - The RAG chain, powered by LangChain, takes each section of a document, retrieves relevant context from the Knowledge Base via Azure AI Search, and constructs prompts tailored for compliance validation. The prompts are sent to the Mistral 3B model (hosted in Azure ML Studio) to determine compliance with legal standards.

4. **Query Decomposition and Result Aggregation**  
   - The backend decomposes each document into sections for granular analysis, allowing for precise compliance checks. Each section’s results are stored and aggregated, providing the frontend with detailed output on compliance status and reasoning.

5. **Deployment**  
   - The backend is hosted on **Azure Container Apps**, ensuring scalability and reliability in processing requests, managing workflows, and handling user interactions seamlessly.

# Proposal

### Integration with Azure Document Intelligence

We propose to integrate our document validation and knowledge base solution into Azure Document Intelligence. This integration will enhance Azure’s existing services by offering users the ability to not only extract text from documents but also evaluate compliance with legal standards.

**Key Benefits:**

- **Comprehensive Tools**: Provides users with streamlined capabilities for document processing and compliance evaluation in one platform.
- **Improved User Experience**: Simplifies workflows by allowing users to manage uploads and validations seamlessly within Azure.
- **Scalability**: Leverages Azure’s robust infrastructure for efficient performance and reliability.

Incorporating our solution will position Azure as a leader in AI-driven document solutions, delivering greater value to users.

# Team

### Team Name: Bitspace

#### Team Members:

- **Aswath T**: [GitHub Profile](https://github.com/t-aswath)
- **Naveen M P**: [GitHub Profile](https://github.com/navi-prem)
- **Rahul Navneeth**: [GitHub Profile](https://github.com/RahulNavneeth)
- **Surya Prakash**: [GitHub Profile](https://github.com/suryaaprakassh)
- **Valan Tamil Dasan**: [GitHub Profile](https://github.com/Valan-Tamil-Dasan)

# Contribution

We welcome contributions and feedback from the community to enhance our document validation solution. Your insights are invaluable in shaping the future of this project. 

- **Contributions**: We encourage developers to contribute code, documentation, and ideas to improve functionality and usability.
- **Feedback**: Please share your thoughts and experiences to help us identify areas for improvement and feature enhancements.
- **Issue Reporting**: If you encounter any issues, we invite you to raise them through our issue tracker, ensuring that we can address them promptly.

Together, we can create a more robust and effective solution for document validation within the Azure ecosystem.


