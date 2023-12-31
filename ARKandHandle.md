# Anatomy of an ARK and Handle request

We received many questions from suppliers on persistent identification. For your convenience we have compiled the following overview that uses ARK and handle.net as an example.

The anatomy of an ARK persistent identifier is comparable to that of Handle. 

In `ark:/60537/by6i35` the `60537` uniquely represents the institution (in this case "'Gouda Time Machine") and `by6i35` is the identifier that Gouda Time Machine allocated to the digital resource. You are free in the way you generate the identifier as long as it is independent of the software system. The identifier is persistently linked to the resource and it must be able to migrate to any other platform in the future.   

Handle uses the same pattern. In `handle:/10648/b017027e-d0b4-102d-bcf8-003048976d84` the `10648` identifies the institution (in this case the National Archive of the Netherlands) and `b017027e-d0b4-102d-bcf8-003048976d84` is the GUID of the resource they created. 

You need a resolver to find these resources online. A resolver is a software service that runs at a specific web address, which you ask where an identifier can be found. 

The ARK resolver is [https://n2t.net/](https://n2t.net/) while Handle identifiers can be resolved through [http://hdl.handle.net/](http://hdl.handle.net/). The main difference between ARK and Handle is how resolution works. 

ARK is a decentralised system and redirects [https://n2t.net/ark:/60537/by6i35](https://n2t.net/ark:/60537/by6i35)  with an HTTP 302 status code to [https://www.goudatijdmachine.nl/ark:/60537/by6i35](https://www.goudatijdmachine.nl/ark:/60537/by6i35) at that point `goudatijdmachine.nl` is responsible for further internal resolution and redirection of the request to the proper current URL of the resource. The developers of the website implemented a service that redirects the request with another HTTP 302 status code to: [https://www.goudatijdmachine.nl/omeka/s/data/item/31488](https://www.goudatijdmachine.nl/omeka/s/data/item/31488) The ARK Alliance organisation - who maintains the ARK PID system - only stores identifiers of organisations **and not of the individual resources**. ARK expects you to handle those yourself.

Handle on the other hand is a centralised system. You not only join as an organisation, you also register every individual PID to each of your resources. Resolving a request on [http://hdl.handle.net/10648/b017027e-d0b4-102d-bcf8-003048976d84](http://hdl.handle.net/10648/b017027e-d0b4-102d-bcf8-003048976d84) will point the user with a single redirect HTTP 302 directly to [https://www.nationaalarchief.nl/onderzoeken/fotocollectie/b017027e-d0b4-102d-bcf8-003048976d84](https://www.nationaalarchief.nl/onderzoeken/fotocollectie/b017027e-d0b4-102d-bcf8-003048976d84). The advantage is that the site `nationaalarchief.nl` does not need to host a second resolving service. But this comes at a cost. Not only do you pay an annual fee for using handle, you also have to maintain the PIDs in the handle registry. You must file any changes to the redirect URLs to avoid breaking links.

We have noticed that the costs to use Handle are frequently misunderstood. A Handle registration costs about €50 per year. 

Many institutions in the cultural heritage sector use [SURF](https://www.surf.nl/en) (the collaborative organisation for IT in Dutch education and research) to help them. SURF provides a PID-service that uses Handle and charges €493 per year (in 2024) on top of the Handle registration fee. For more information see: [SURF Data Persistent Identifier](https://www.surf.nl/en/data-persistent-identifier-data-always-findable-by-permanent-references). The SURF service allows you to automatically generate and administer PIDs for any resource located in SURF systems. ***It cannot provide this service for resources located elsewhere.*** 

NDE does not require you to make use of the SURF service when you chose Handle as your PID-system. 

Be aware that you need to know the storage location of the resources that you want to share with the NDE network, in order to decide if the SURF PID-service provides you with value. We have encountered organisations who paid for the SURF-service while none of their (linked data) resources were stored there. 
