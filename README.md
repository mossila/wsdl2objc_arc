wsdl2objc_arc
=============

A fork project from https://code.google.com/p/wsdl2objc/  to use without -fno-objc-arc.

#Usage
1. Clone and Build & Run
2. Parse WSDL 
3. Drop output to iOS project
4. Go to `Build Pharses` add `libxml2` to `Link Binary with Libraries`
5. Go to `Build Settings` add `/usr/include/libxml2` to `Header search paths`

#Example
```
#import "ServiceNameSvc.h"
...
@interface MyClass<ServiceNameSoapBindingResponseDelegate>
...
-(void) callService {
    ServiceNameSoapBinding *service = [[ServiceNameSoapBinding alloc] initWithAddress:@"http://example-service.com"] ;
    service.logXMLInOut = NO;
    ServiceNameSvc_SubService *request = [ServiceNameSvc_SubService] ;
    request.parameterName = @"request argument";
    [service SubServiceAsyncUsingParameters:request delegate:self];
}
-(void)operation:(ServiceNameSoapBindingOperation *)operation completedWithResponse:(ServiceNameSoapBindingResponse *)response {
    NSArray *responseBodyParts = response.bodyParts;
    for(id bodyPart in responseBodyParts) {
        if([bodyPart isKindOfClass:[ServiceNameSvc_SubServiceResponse class]]) {
            [self processResponseData:operation.responseData];
        }
    }
}
-(void) processResponseData:(NSData*) responseData {
	//use response data here
}
```

# Found bug
Feel free to discuss with me. @mossila