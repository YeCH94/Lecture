# XML

------

### XML이란?

- eXtensibleMarkupLanguage의 약자
- HTML과 흡사한 마크업 language
- 데이터를 전송 및 저장하도록 설계됨
- XML 태그는 미리 정의되지 않음
- W3C 표준을 따름

### XML vs HTML

- XML은 HTML을 대체하지 않음
- XML은 데이터를 전송하고 저장하도록 설계되었지만 HTML은 데이터를 보여주기 위해 설계

### XML은 무엇인가?

- XML은 HTML에서 데이터를 분리시킴.
- 데이터 공유를 단순화하는 XML
- XML은 새로운 인터넷 언어를 만드는 데 사용.

### XML Syntax Rules

- 모든 XML 요소는 닫는 태그를 가져야 함.

- XML 태그는 대소문자를 구별함.

- XML 요소는 올바르게 중첩되어야 함. (마지막에 열어준 태그를 처음으로 닫고 그 다음으로!)

- XML 문서는 루트 요소를 가져야 함.

- XML 속성 값은 “를 붙여야 함.

- 주석은 <!-- -->

- 기본 엔티티

  ```
  &lt; <
  &gt; >
  &amp; &
  &apos; '
  &quot; "
  ```

### XML Elements

- 태그가 열린 곳부터 닫힌 곳까지 요소!
- 태그 열기/닫기
- Element에 포함 가능한 것
  - Text
  - Attributes
  - Other elements
  - Mix of all of the above

### XML Naming Rules

- 문자, 숫자 및 기타 문자 포함
- 숫자 또는 구두점(?!,.)으로 시작하지 말 것
- xml로 시작하지 말 것(‘XML’, ‘Xml’ 또한 마찬가지)
- 공백과 특수 문자를 포함하지 말 것

### XML Attributes

- 속성은 요소의 추가 정보를 제공
- 따옴표로 묶여야 함
- 여러 value를 가질 수 없음
- 트리 구조를 가질 수 없음
- 쉽게 확장 불가
- 권장사항
  - 메타데이터를 속성으로
  - 데이터 자체를 Element로

### Well-formed XML

- XML 문서는 루트 element를 가져야 함
- XML element는 닫는 태그가 있어야 함.
- XML 태그는 대소문자를 구별함.
- XML element는 올바르게 중첩되어야 함.
- XML attribute 값은 따옴표로 묶어야 함.

### DTD

- XML 문서의 올바른 building block

- Internal DTD 선언

  ```xml-dtd
  <!DOCTYPE name [DTD 선언문]>
  ```

- External DTD 선언

  ```xml-dtd
  <!DOCTYPE name SYSTEM “File dir">
  ```

- PCDATA vs CDATA

  - PCDATA – XML 파서에 의해 파싱되는 데이터 (XML 태그 및 문법에 사용되는 문자 포함 불가)

  - CDATA – XML 파서가 파싱하지 않는 데이터

    - 사용법 : 

      ```xml-dtd
      <![CDATA[“내용”]]>
      ```

- Element 선언

  ```xml-dtd
  <!ELEMENT name category>
  ```

  - category는 EMPTY, ANY

  ```xml-dtd
  <!ELEMENT name (content)>
  ```

  - Content에는 #PCDATA 또는 다른 Element(s)가 옴

  - Content에 하위 Element가 왔을 때 출현 빈도 설정(기본값은 1개)

    - +는 1 또는 그 이상

    - *는 0 또는 그 이상

    - ?는 0 또는 1

  ```xml-dtd
  <!ELEMENT note (to,from,header,(message|body))>
  ```
  
  - 와 같이 | 를 통해 either/or 가능

- Attribute 선언

  ```xml-dtd
  <!ATTLIST element-name attribute-name attribute-type default-value>
  ```

  - Attribute-type
    - CDATA, ENTITY, 그 외 것들 (PCDATA는 Attribute의 값으로 못 씀)
  - Default-value
    - Value : 기본값 설정 (ex : “Default”)
    - #REQUIRED : 필수로 써야 하는 attribute
    - #IMPLIED : 써도 되고 안써도 되는 attribute
    - #FIXED value : value로 값이 고정됨.

- Entity 선언

  - 텍스트 혹은 특수 문자에 대한 바로 가기를 정의하는데 사용

    ```xml-dtd
    <!ENTITY entity-name “entity-value">
    ```

    Internal 선언

  - XML 내에서 &entity-name;으로 사용

    ```xml-dtd
    <!ENTITY entity-name SYSTEM “URI/URL">
    ```

    External 선언

### XML Schema

- DTD의 대안으로 XML 기반
- XML 구문을 사용
- XML 문서의 구조 정의
- XML Schema 언어는 XSD
- DTD보다 강력함
- 데이터 유형 및 네임 스페이스 지원
- Root element <schema> - XSD
  - Attributes
    - xmlns:xs=”<http://www.w3.org/2001/XMLSchema>”
      - 저 주소에 있는 스키마를 가져와서 xs라는 네임스페이스로 쓸거다.
    - targetNamespace=”<http://www.w3schools.com>”
      - 이 스키마에 정의된 element는 저 주소의 네임스페이스에서 가져오는 거야
    - xmlns=”<http://www.w3schools.com>”
      - 기본 네임스페이스는 저 주소야
    - elementFormDefault=”qualified”
      - 이 스키마의 모든 element가 XML 문서에서 사용될 때 정규화 되어야 해

- Referring a schema – XML 문서
  - Root Attributes
    - xmlns=”http://www.w3schools.com”
      - 이 XML 문서에서 사용되는 element는 저 네임스페이스에 선언되어 있어
    - xmlns:xsi=”http://www.w3.org/2001/XMLSchema-instance”
      - XML 스키마 인스턴스 네임스페이스
    - xsi:schemaLocation=”http://www.w3schools.com note.xsd”
      - 띄어쓰기 기준으로 앞에거는 네임스페이스, 뒤에거는 스키마의 주소

- Simple Element

  - 다른 하위 element 또는 attribute 없이 텍스트만 포함할 수 있는 element

  - 텍스트는 다양한 타입을 가짐

    - xs:string, xs:decimal, xs:integer, xs:Boolean, xs:date, xs:time, etc
    - 사용자 정의된 커스텀 타입

  - 선언

    ```xml
    <xs:element name=”xxx” type=”yyy”/>
    ```

  - 기본 및 고정 값

    ```xml
    <xs:element name=”xxx” type=”yyy” default=”zzz”/>
    ```

    ```xml
    <xs:element name=”xxx” type=”yyy” fixed=”zzz”/>
    ```

- Restrictions/Facets

  - Value의 제한 → 이 범위 안에서만 값이 나와야 해

    ```xml
    <xs:element name="age">
    	<xs:simpleType>
    		<xs:restriction base="xs:integer"> 
    			<xs:minInclusive value="0"/> 
    			<xs:maxInclusive value="120"/>
    		</xs:restriction>
    	</xs:simpleType>
    </xs:element>
    ```

  - Value의 집합 제한 → 값은 얘네만 될 수 있어

    ```xml
    <xs:element name="car">
    	<xs:simpleType>
    		<xs:restriction base="xs:string"> 
    			<xs:enumeration value="Audi"/> 
    			<xs:enumeration value="Benz"/> 
    			<xs:enumeration value="BMW"/>
    		</xs:restriction>
    	</xs:simpleType>
    </xs:element>
    ```

  - 일련의 Value에 대한 제한 → value의 내용은 이 안에 있는 걸로만 구성되어야 해

    ```xml
    <xs:element name="letter">
    	<xs:simpleType>
    		<xs:restriction base="xs:string">
    			<xs:pattern value="[a-z]"/>
    		</xs:restriction>
    	</xs:simpleType>
    </xs:element>
    ```

  - 데이터 타입

![img](file:///C:/Users/CH/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

- Attribute

  ```xml
  <xs:attribute name=”xxx” type=”yyy”/>
  ```
  - Simple element와 마찬가지로 name, type, default, fixed를 가짐
  - 추가로 use를 가짐 (기본값은 optional이고 이 경우 쓰지 않아도 된다)
    - required : 이 attribute는 꼭 선언되어야 해
    - optional : 이 attribute는 써도 되고 안 써도 돼. (DTD의 #IMPLIED와 같음)