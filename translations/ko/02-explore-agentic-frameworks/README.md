# AI 에이전트 프레임워크 탐구하기 (~4/9)

AI 에이전트 프레임워크는 AI 에이전트를 쉽게 생성, 배포, 관리할 수 있도록 설계된 소프트웨어 플랫폼입니다. 이러한 프레임워크는 개발자들에게 사전 구축된 컴포넌트, 추상화 및 도구를 제공하여 복잡한 AI 시스템 개발을 간소화합니다.
이 프레임워크는 AI 에이전트 개발에서 공통적으로 발생하는 문제를 표준화된 방식으로 해결하여 개발자가 애플리케이션의 고유한 측면에 집중할 수 있도록 돕습니다. 이를 통해 AI 시스템 구축에서 확장성, 접근성, 효율성이 향상됩니다.

## 소개

이번 강의에서는 다음을 다룹니다:

- AI 에이전트 프레임워크란 무엇이며, 개발자들이 이를 통해 무엇을 할 수 있는가?
- 팀이 이를 사용하여 에이전트의 기능을 빠르게 프로토타입하고, 반복하고, 개선할 수 있는 방법은 무엇인가?
- Microsoft에서 제공하는 프레임워크 및 도구([Autogen](https://aka.ms/ai-agents/autogen) / [Semantic Kernel](https://aka.ms/ai-agents-beginners/semantic-kernel) / [Azure AI Agent Service](https://aka.ms/ai-agents-beginners/ai-agent-service)) 간의 차이점은 무엇인가?
- 기존 Azure 에코시스템 도구를 직접 통합할 수 있는가, 아니면 별도의 솔루션이 필요한가?
- Azure AI Agents 서비스란 무엇이며, 이것이 어떻게 도움이 되는가?

## 학습 목표

이번 강의의 목표는 다음을 이해하는 것입니다:

- AI 에이전트 프레임워크가 AI 개발에서 가지는 역할.
- AI 에이전트 프레임워크를 활용하여 지능형 에이전트를 구축하는 방법.
- AI 에이전트 프레임워크로 활성화되는 주요 기능.
- Autogen, Semantic Kernel, Azure AI Agent Service 간의 차이점.

## AI 에이전트 프레임워크란 무엇이며, 개발자들이 이를 통해 무엇을 할 수 있는가?

전통적인 AI 프레임워크는 AI를 앱에 통합하고 앱의 성능을 다음과 같은 방식으로 향상시킬 수 있도록 도와줍니다:

- **개인화**: AI는 사용자 행동과 선호도를 분석하여 개인화된 추천, 콘텐츠, 경험을 제공합니다.  
  예: Netflix와 같은 스트리밍 서비스는 시청 기록을 기반으로 영화를 추천하여 사용자 만족도를 높입니다.
- **자동화 및 효율성**: AI는 반복적인 작업을 자동화하고 워크플로를 간소화하며 운영 효율성을 향상시킬 수 있습니다.  
  예: 고객 서비스 앱은 AI 기반 챗봇을 활용하여 일반적인 문의를 처리하고, 응답 시간을 단축하며, 복잡한 문제는 인간 상담원이 처리할 수 있도록 합니다.
- **향상된 사용자 경험**: AI는 음성 인식, 자연어 처리, 예측 텍스트와 같은 지능형 기능을 제공하여 전반적인 사용자 경험을 개선합니다.  
  예: Siri와 Google Assistant와 같은 가상 비서는 AI를 활용하여 음성 명령을 이해하고 응답하여 사용자와의 상호작용을 더 쉽게 만듭니다.

### 모두 훌륭해 보이지만, 왜 AI 에이전트 프레임워크가 필요한가요?

AI 에이전트 프레임워크는 단순한 AI 프레임워크 이상의 것을 제공합니다. 이 프레임워크는 사용자가 지정한 목표를 달성하기 위해 사용자, 다른 에이전트, 환경과 상호작용할 수 있는 지능형 에이전트를 생성할 수 있도록 설계되었습니다. 이러한 에이전트는 자율적으로 행동하고, 의사 결정을 내리며, 변화하는 상황에 적응할 수 있습니다. 다음은 AI 에이전트 프레임워크가 제공하는 주요 기능입니다:

- **에이전트 간 협업 및 조정**: 여러 AI 에이전트를 생성하여 협력, 커뮤니케이션, 조정을 통해 복잡한 작업을 해결할 수 있습니다.
- **작업 자동화 및 관리**: 다단계 워크플로의 자동화, 작업 위임, 에이전트 간 동적 작업 관리를 위한 메커니즘을 제공합니다.
- **맥락 이해 및 적응**: 에이전트가 맥락을 이해하고, 변화하는 환경에 적응하며, 실시간 정보를 기반으로 의사 결정을 내릴 수 있는 기능을 제공합니다.

결론적으로, 에이전트는 더 많은 일을 가능하게 하고, 자동화를 한 단계 더 발전시키며, 환경에서 학습하고 적응할 수 있는 더 지능적인 시스템을 만들 수 있게 합니다.

## 에이전트의 기능을 빠르게 프로토타입하고, 반복하고, 개선하는 방법은?

이 분야는 빠르게 발전하고 있지만, 대부분의 AI 에이전트 프레임워크에서 공통적으로 활용할 수 있는 몇 가지 요소가 있습니다. 모듈형 컴포넌트, 협업 도구, 실시간 학습이 그 예입니다. 자세히 살펴보겠습니다:

- **모듈형 컴포넌트 사용**: AI 프레임워크는 프롬프트, 파서, 메모리 관리와 같은 사전 구축된 컴포넌트를 제공합니다.
- **협업 도구 활용**: 특정 역할과 작업을 가진 에이전트를 설계하여 협업 워크플로를 테스트하고 개선할 수 있습니다.
- **실시간 학습**: 피드백 루프를 구현하여 에이전트가 상호작용에서 학습하고 동적으로 행동을 조정하도록 합니다.

### 모듈형 컴포넌트 사용

LangChain 및 Microsoft Semantic Kernel과 같은 프레임워크는 프롬프트, 파서, 메모리 관리와 같은 사전 구축된 컴포넌트를 제공합니다.

**팀이 이를 사용하는 방법**: 팀은 이러한 컴포넌트를 빠르게 조립하여 기능적인 프로토타입을 만들 수 있습니다. 이는 처음부터 시작하지 않고도 빠르게 실험하고 반복할 수 있도록 합니다.

**실제 작동 방식**: 사전 구축된 파서를 사용하여 사용자 입력에서 정보를 추출하거나, 메모리 모듈을 사용하여 데이터를 저장 및 검색하거나, 프롬프트 생성기를 사용하여 사용자와 상호작용할 수 있습니다. 이를 통해 고수준의 논리에 집중할 수 있습니다.

**예제 코드**. 사용자 입력에서 정보를 추출하기 위해 사전 구축된 파서를 사용하는 예제를 살펴보겠습니다:

```python
from langchain import Parser

parser = Parser()
user_input = "Book a flight from New York to London on July 15th"

parsed_data = parser.parse(user_input)

print(parsed_data)
# Output: {'origin': 'New York', 'destination': 'London', 'date': 'July 15th'}
```

이 예제에서 볼 수 있듯이, 사전 구축된 파서를 활용하여 비행 예약 요청의 출발지, 목적지, 날짜와 같은 주요 정보를 추출할 수 있습니다. 이러한 모듈형 접근 방식은 고수준의 논리에 집중할 수 있게 합니다.

### 협업 도구 활용

CrewAI 및 Microsoft Autogen과 같은 프레임워크는 여러 에이전트를 생성하여 협력할 수 있도록 지원합니다.

**팀이 이를 사용하는 방법**: 팀은 특정 역할과 작업을 가진 에이전트를 설계하여 협업 워크플로를 테스트하고 개선하며, 전체 시스템 효율성을 높일 수 있습니다.

**실제 작동 방식**: 데이터 검색, 분석, 의사 결정과 같은 특정 기능을 가진 에이전트 팀을 생성할 수 있습니다. 이러한 에이전트는 정보를 공유하고 사용자 질의에 응답하거나 작업을 완료하기 위해 협력할 수 있습니다.

**예제 코드 (Autogen)**:

```python
# creating agents, then create a round robin schedule where they can work together, in this case in order

# Data Retrieval Agent
# Data Analysis Agent
# Decision Making Agent

agent_retrieve = AssistantAgent(
    name="dataretrieval",
    model_client=model_client,
    tools=[retrieve_tool],
    system_message="Use tools to solve tasks."
)

agent_analyze = AssistantAgent(
    name="dataanalysis",
    model_client=model_client,
    tools=[analyze_tool],
    system_message="Use tools to solve tasks."
)

# conversation ends when user says "APPROVE"
termination = TextMentionTermination("APPROVE")

user_proxy = UserProxyAgent("user_proxy", input_func=input)

team = RoundRobinGroupChat([agent_retrieve, agent_analyze, user_proxy], termination_condition=termination)

stream = team.run_stream(task="Analyze data", max_turns=10)
# Use asyncio.run(...) when running in a script.
await Console(stream)
```

위 코드에서 볼 수 있듯이, 여러 에이전트가 데이터를 분석하는 작업을 함께 수행하도록 설계할 수 있습니다. 각 에이전트는 특정 기능을 수행하며, 협력을 통해 원하는 결과를 달성합니다. 특정 역할을 가진 에이전트를 생성함으로써 작업 효율성과 성능을 향상시킬 수 있습니다.

### 실시간 학습

고급 프레임워크는 실시간 맥락 이해 및 적응 기능을 제공합니다.

**팀이 이를 사용하는 방법**: 팀은 피드백 루프를 구현하여 에이전트가 상호작용에서 학습하고 동적으로 행동을 조정하도록 하여 지속적으로 능력을 개선하고 정제할 수 있습니다.

**실제 작동 방식**: 에이전트는 사용자 피드백, 환경 데이터, 작업 결과를 분석하여 지식 기반을 업데이트하고, 의사 결정 알고리즘을 조정하며, 성능을 개선합니다. 이러한 반복 학습 프로세스를 통해 에이전트는 변화하는 조건과 사용자 선호도에 적응하며, 시스템의 전반적인 효과를 향상시킬 수 있습니다.

## Autogen, Semantic Kernel, Azure AI Agent Service 간의 차이점은 무엇인가?

이 프레임워크들을 비교하는 방법은 여러 가지가 있지만, 설계, 기능, 주요 사용 사례 측면에서 몇 가지 핵심 차이점을 살펴보겠습니다:

## Autogen

Microsoft Research의 AI Frontiers Lab에서 개발한 오픈소스 프레임워크입니다. 이벤트 기반, 분산된 *에이전트 기반* 애플리케이션에 중점을 두며, 여러 LLM 및 SLM, 도구, 고급 다중 에이전트 설계 패턴을 지원합니다.

Autogen은 에이전트를 중심으로 설계되었습니다. 에이전트는 환경을 인식하고, 의사 결정을 내리고, 특정 목표를 달성하기 위해 행동하는 자율적인 엔터티입니다. 에이전트는 비동기 메시지를 통해 통신하여 독립적이고 병렬로 작업할 수 있으며, 시스템의 확장성과 응답성을 향상시킵니다.

에이전트는 [액터 모델](https://en.wikipedia.org/wiki/Actor_model)을 기반으로 합니다. Wikipedia에 따르면, 액터는 _동시 계산의 기본 구성 요소로서, 수신된 메시지에 응답하여 로컬 결정을 내리고, 새로운 액터를 생성하며, 메시지를 보내고, 다음 메시지에 어떻게 응답할지 결정할 수 있습니다._

**사용 사례**: 코드 생성 자동화, 데이터 분석 작업, 계획 및 연구 기능을 위한 맞춤형 에이전트 구축.

Autogen의 핵심 개념에 대한 설명은 계속됩니다...
```
```markdown
프로젝트 목표를 기반으로 합니다. 자연어 이해 및 콘텐츠 생성에 이상적입니다.  
- **Azure AI Agent Service**: 유연한 모델, 엔터프라이즈 보안 메커니즘, 데이터 저장 방법. 엔터프라이즈 애플리케이션에서 안전하고 확장 가능하며 유연한 AI 에이전트 배포에 이상적입니다.

## 기존 Azure 에코시스템 도구를 직접 통합할 수 있나요, 아니면 독립형 솔루션이 필요하나요?
답은 예입니다. Azure AI Agent Service는 다른 Azure 서비스와 원활하게 작동하도록 설계되었기 때문에 기존 Azure 에코시스템 도구를 직접 통합할 수 있습니다. 예를 들어 Bing, Azure AI Search, Azure Functions를 통합할 수 있습니다. 또한 Azure AI Foundry와 깊은 통합이 가능합니다.  

Autogen 및 Semantic Kernel의 경우에도 Azure 서비스와 통합할 수 있지만, 이를 위해 코드에서 Azure 서비스를 호출해야 할 수 있습니다. 또 다른 통합 방법은 Azure SDK를 사용하여 에이전트에서 Azure 서비스와 상호 작용하는 것입니다.  

추가적으로, 앞서 언급했듯이 Autogen 또는 Semantic Kernel에서 구축된 에이전트를 위한 오케스트레이터로 Azure AI Agent Service를 사용할 수 있으며, 이를 통해 Azure 에코시스템에 쉽게 접근할 수 있습니다.

## 참고 문헌
- [1] - [Azure Agent Service](https://techcommunity.microsoft.com/blog/azure-ai-services-blog/introducing-azure-ai-agent-service/4298357)  
- [2] - [Semantic Kernel and Autogen](https://devblogs.microsoft.com/semantic-kernel/microsofts-agentic-ai-frameworks-autogen-and-semantic-kernel/)  
- [3] - [Semantic Kernel Agent Framework](https://learn.microsoft.com/semantic-kernel/frameworks/agent/?pivots=programming-language-csharp)  
- [4] - [Azure AI Agent service](https://learn.microsoft.com/azure/ai-services/agents/overview)  
- [5] - [Using Azure AI Agent Service with AutoGen / Semantic Kernel to build a multi-agent's solution](https://techcommunity.microsoft.com/blog/educatordeveloperblog/using-azure-ai-agent-service-with-autogen--semantic-kernel-to-build-a-multi-agen/4363121)
```

**면책 조항**:  
이 문서는 기계 기반 AI 번역 서비스를 사용하여 번역되었습니다. 정확성을 위해 최선을 다하고 있지만, 자동 번역에는 오류나 부정확성이 포함될 수 있습니다. 원본 문서의 모국어 버전을 권위 있는 출처로 간주해야 합니다. 중요한 정보에 대해서는 전문적인 인간 번역을 권장합니다. 이 번역 사용으로 인해 발생하는 오해나 잘못된 해석에 대해 당사는 책임을 지지 않습니다.
