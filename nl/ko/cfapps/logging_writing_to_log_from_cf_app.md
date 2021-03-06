---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, logging

subcollection: cloudloganalysis

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# CF 앱을 통한 런타임 애플리케이션 로깅
{: #logging_writing_to_log_from_cf_app}

{{site.data.keyword.Bluemix}}에서 Cloud Foundry 앱과 해당 런타임에 대한 로그 데이터를 지속하려면 STDOUT 및 STDERR에 로그를 작성해야 합니다. 
{:shortdesc}

{{site.data.keyword.Bluemix_notm}}에서 STDOUT 및 STDERR 로그 레코드가 자동으로 수집됩니다.

* STDOUT(표준 출력)은 일반 정보를 제공합니다.  
* STDERR(표준 오류)은 오류 메시지 및 기타 진단 경고를 포함하는 정보를 제공합니다. 

Loggregator는 표준 출력 및 표준 오류 데이터를 자동으로 선택합니다. Loggregator는 Cloud Foundry의 내부에서 로그를 전달하는 컴포넌트입니다. 

예: 

**Liberty Cloud Foundry 앱**의 경우, Liberty 서버에 대한 기본 console.log가 loggregator에 의해 자동으로 선택됩니다. 

* console.log에는 JVM 프로세스에서 경로 재지정된 STDOUT 및 STDERR이 포함되어 있습니다. 기본 consoleLogLevel 구성을 사용하는 경우, 콘솔 출력에는 주요 이벤트 및 오류가 포함되어 있습니다. 기본 copySystemStreams 구성을 사용하는 경우 콘솔 출력에는 system.out 및 system.err 스트림에 작성된 메시지도 포함됩니다. 콘솔 출력에는 JVM 프로세스에 의해 직접 작성되는 메시지(예: -verbose:gc 출력)가 항상 포함됩니다. server.xml을 통해 Liberty의 로깅 레벨을 조정할 수 있습니다.
* consoleLogLevel은 console.log 핸들러의 필터 레벨을 설정합니다. consoleLogLevel을 INFO로 설정할 때는 모든 INFO, AUDIT, WARNING 및 ERROR 메시지가 console.log 파일에 작성되도록 구성합니다. **참고:** FINE, FINER, FINEST 로그 항목은 trace.log 파일에만 작성됩니다.

Liberty for Java™ 애플리케이션에 대한 자세한 정보는 [Liberty Profile: Logging and Trace ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}를 참조하십시오.

**Node.js Cloud Foundry 앱**의 경우, 기본 제공 콘솔 로깅 모듈을 사용하여 {{site.data.keyword.Bluemix}}에서 런타임에 대한 로깅을 구성할 수 있습니다. stdout와 stderr에 모두 메시지를 넣을 수 있습니다.

* console.log('message')는 STDOUT 스트림에 메시지 전송
* console.error('error_message')는 STDERR 스트림에 오류 전송

Node.js 애플리케이션에 대한 자세한 정보는 [How to log in node.js ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.nodejitsu.com/articles/intermediate/how-to-log/){: new_window}를 참조하십시오.


**Ruby on Rails 애플리케이션**에 대한 자세한 정보는 [The Logger ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}를 참조하십시오.

일부 애플리케이션 런타임 로그와 Loggregator에서 자동으로 선택되는 로그 사이의 맵핑이 다음 표에 나열되어 있습니다.

|**런타임** |**STDOUT**     |**STDERR** |
|-----------------|-------------------|-------------------|
|Liberty |system.out |system.err |
|Node.js |console.log, console.info |console.error, console.warn |
|Ruby |stdout|stderr |
{: caption="표 1. 일부 애플리케이션 런타임 로그와 Loggregator에서 자동으로 선택되는 로그 사이의 맵핑" caption-side="top"}

