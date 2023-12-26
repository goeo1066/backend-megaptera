---
description: 직렬화
---

# Serialization

> [Serialization](https://en.wikipedia.org/wiki/Serialization)
>
> _In computing, serialization (or serialisation) is the process of translating a_ [_data structure_](https://en.wikipedia.org/wiki/Data\_structure) _or_ [_object_](https://en.wikipedia.org/wiki/Object\_\(computer\_science\)) _state into a format that can be stored (e.g._ [_files_](https://en.wikipedia.org/wiki/Computer\_file) _in_ [_secondary storage devices_](https://en.wikipedia.org/wiki/Secondary\_storage\_devices)_,_ [_data buffers_](https://en.wikipedia.org/wiki/Data\_buffer) _in primary storage devices) or transmitted (e.g._ [_data streams_](https://en.wikipedia.org/wiki/Data\_stream) _over_ [_computer networks_](https://en.wikipedia.org/wiki/Computer\_networks)_) and reconstructed later (possibly in a different computer environment)_

> Deserialization (also called unserialization or [unmarshalling](https://en.wikipedia.org/wiki/Unmarshalling))
>
> T_his process of serializing an object is also called_ [_marshalling_](https://en.wikipedia.org/wiki/Marshalling\_\(computer\_science\)) _an object in some situations._[_\[2\]_](https://en.wikipedia.org/wiki/Serialization#cite\_note-2)[_\[3\]_](https://en.wikipedia.org/wiki/Serialization#cite\_note-ocaml-3)[_\[4\]_](https://en.wikipedia.org/wiki/Serialization#cite\_note-4) _The opposite operation, extracting a data structure from a series of bytes, is deserialization, (also called unserialization or_ [_unmarshalling_](https://en.wikipedia.org/wiki/Unmarshalling)_)._

> [Marshalling](https://en.wikipedia.org/wiki/Marshalling\_\(computer\_science\))
>
> _In the_ [_Java_](https://en.wikipedia.org/wiki/Java\_\(programming\_language\))_-related_ [_RFC_](https://en.wikipedia.org/wiki/RFC\_\(identifier\)) [_2713_](https://datatracker.ietf.org/doc/html/rfc2713)_, marshalling is used when serializing objects for_ [_remote invocation_](https://en.wikipedia.org/wiki/Remote\_procedure\_call)_. An object that is marshalled records the state of the original object and it contains the codebase (codebase here refers to a list of URLs where the object code can be loaded from, and not source code)._&#x20;
>
> 각 언어마다 마샬링의 의미가 조금씩 다르다.&#x20;

저장이나 전송에 적합하도록 변환(Translating)하는 작업

* 메모리상의 데이터 구조나 객체(Object)를 파일, DB 등에 저장하거나 네트워크를 통해 전송이 가능하도록 변환
* 복구도 가능하다.
* Binary, Text(XML, JSON, YAML 등)

## [JSON](https://en.wikipedia.org/wiki/JSON) (JavaScript Object Notation)

[JSON 개요](https://www.json.org/json-ko.html)

* 사람이 읽고 쓰기 쉽고, 기계가 분석하고 생성하기_도_ 쉽다.
*
