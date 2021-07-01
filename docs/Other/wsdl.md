---
title: WSDL Glossary
---
## What is WSDL

Web services description language (WSDL) is an XML document that describes a web service. WSDL is often pronounced "wizdul". 
It describes what operations a web service provides, the structure of the messages it sends and receives, and how to send 
those messages. This article is a very brief overview of the common WSDL elements. If you are new to WSDL, you may prefer 
to read [Understanding WSDL](https://msdn.microsoft.com/en-us/library/ms996486.aspx "Understanding WSDL").

## Core WSDL Elements
### Definition

The `<definitions>` element is the WSDL's root XML element. It typically contains several other elements including 
[types](#types) , [message](#message), [portType](#portType), [binding](#binding) and [service](#service).

### Types
The `<types>` element contains XML schema type definitions (xsd). The xsd's describe the structure of the XML sent and 
received by the web service.

### Message
A message is an XML document that can be sent or received by the web service. A message is usually associated with one 
or more [operation](#operation). For example, an operation to `createNewOrder` might have an input message `newOrder` 
and an output message `orderStatus`.

### PortType (Interfac
The `<portType>` element is best thought of as an interface, and will be renamed as such in version 1.2 of the WSDL 
specification. It contains one or more `<operation>` elements.

### Operation
An `<operation>` element defines an operation with the web service. It groups together the [message](#message) elements 
that can be passed to or from the web service. An operation can have an input and output message (request-response), or 
it can just define an input message (one-way), send an output message only (notification) or send an output message to 
ask for an input message (solicit-response). The operation may also define a fault message too.

### Binding
A `<binding>` element is a collection of one or more `operations`. It describes how an operation is implemented. It 
defines the communication protocol (e.g. http), style of service (document or rpc), and the `SOAPAction` HTTP header for 
the defined operations.

### Document & RPC
The document style indicates that the SOAP body will contain an XML document (and is able to be validated by the previously 
defined xsd's). An RPC style indicates that the SOAP body will contain an XML representation of a method call. It includes 
the method name and parameters of the method to generate the XML structure. Follow this link for a more in-depth discussion 
on [Document and RPC style web services](http://java.globinch.com/enterprise-java/web-services/soap-binding-document-rpc-style-web-services-difference/ "Document vs RPC")

### Service
The `<service>` element defines the endpoint (port) that exposes a particular binding. I.e. the URL to use to call an 
operation within the binding

### Example WSDL Document
```xml
<definitions name="EndorsementSearch"  
 targetNamespace="http://namespaces.snowboard-info.com"  
 xmlns:es="http://www.snowboard-info.com/EndorsementSearch.wsdl"  
 xmlns:esxsd="http://schemas.snowboard-info.com/EndorsementSearch.xsd"  
 xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"  
 xmlns="http://schemas.xmlsoap.org/wsdl/"  
>  
  
 <!-- omitted types section with content model schema info \-->  
  
 <message name="GetEndorsingBoarderRequest">  
  <part name="body" element="esxsd:GetEndorsingBoarder"/>  
 </message>  
  
 <message name="GetEndorsingBoarderResponse">  
  <part name="body" element="esxsd:GetEndorsingBoarderResponse"/>  
 </message>  
  
 <portType name="GetEndorsingBoarderPortType">  
  <operation name="GetEndorsingBoarder">  
   <input message="es:GetEndorsingBoarderRequest"/>  
   <output message="es:GetEndorsingBoarderResponse"/>  
   <fault message="es:GetEndorsingBoarderFault"/>  
  </operation>  
 </portType>  
  
 <binding name="EndorsementSearchSoapBinding" type="es:GetEndorsingBoarderPortType">  
  <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>  
  <operation name="GetEndorsingBoarder">  
   <soap:operation soapAction="http://www.snowboard-info.com/EndorsementSearch"/>  
   <input>  
    <soap:body use="literal" 
                   namespace="http://schemas.snowboard-info.com/EndorsementSearch.xsd"/>  
   </input>  
   <output>  
    <soap:body use="literal" 
                   namespace="http://schemas.snowboard-info.com/EndorsementSearch.xsd"/>  
   </output>  
   <fault>  
    <soap:body use="literal" 
                   namespace="http://schemas.snowboard-info.com/EndorsementSearch.xsd"/>  
   </fault>  
  </operation>  
 </binding>  
  
 <service name="EndorsementSearchService">  
  <documentation>snowboarding\-info.com Endorsement Service</documentation>  
  <port name="GetEndorsingBoarderPort" binding="es:EndorsementSearchSoapBinding">  
   <soap:address location="http://www.snowboard-info.com/EndorsementSearch"/>  
  </port>  
 </service>  
</definitions>
```