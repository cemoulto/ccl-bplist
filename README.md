# ccl-bplist
Automatically exported from code.google.com/p/ccl-bplist

<td id="wikicontent" class="psdescription">
 <p><strong>ccl_bplist is a small Python module for dealing with binary property lists (bplists). It also contains special helper functionality to simplify the processing of NSKeyedArchiver structures often found in binary property lists.</strong> </p><p><i>To download the scripts go to the "Source" tab and click "Browse"</i> </p><p><i>A quick-start guide can be found below</i> </p><p>It converts the binary property list file contents into a native Python object. </p><p></p><table class="wikitable"><tbody><tr><td style="border: 1px solid #ccc; padding: 5px;"><i>Property List Type</i></td><td style="border: 1px solid #ccc; padding: 5px;"><i>Returned Python Type</i></td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">null</td><td style="border: 1px solid #ccc; padding: 5px;">None</td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">true</td><td style="border: 1px solid #ccc; padding: 5px;">True</td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">false</td><td style="border: 1px solid #ccc; padding: 5px;">False</td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">integer</td><td style="border: 1px solid #ccc; padding: 5px;">int</td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">real</td><td style="border: 1px solid #ccc; padding: 5px;">float</td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">uid</td><td style="border: 1px solid #ccc; padding: 5px;">int</td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">date</td><td style="border: 1px solid #ccc; padding: 5px;">datetime.datetime</td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">string</td><td style="border: 1px solid #ccc; padding: 5px;">str</td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">data</td><td style="border: 1px solid #ccc; padding: 5px;">bytes</td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">array</td><td style="border: 1px solid #ccc; padding: 5px;">list</td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">dict</td><td style="border: 1px solid #ccc; padding: 5px;">dict</td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">set</td><td style="border: 1px solid #ccc; padding: 5px;">list</td></tr> </tbody></table><p></p><hr><h2><a name="Quick-Start"></a>Quick-Start<a href="#Quick-Start" class="section_anchor"></a></h2><p>Here's a quick overview of the module's features: </p><h3><a name="Opening_Property_Lists"></a>Opening Property Lists<a href="#Opening_Property_Lists" class="section_anchor"></a></h3><p>At its most basic, just import the module, create a file-like object around your plist (here I'm opening a file, but often I find that I'm dealing with embedded plists, in which case <tt>io.BytesIO</tt> is very useful). </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> </span><span class="kwd">import</span><span class="pln"> ccl_bplist<br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> f </span><span class="pun">=</span><span class="pln"> open</span><span class="pun">(</span><span class="str">"plist.plist"</span><span class="pun">,</span><span class="pln"> </span><span class="str">"rb"</span><span class="pun">)</span><span class="pln"><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> plist </span><span class="pun">=</span><span class="pln"> ccl_bplist</span><span class="pun">.</span><span class="pln">load</span><span class="pun">(</span><span class="pln">f</span><span class="pun">)</span><span class="pln"><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> <br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> plist<br></span><span class="pun">{</span><span class="str">'$objects'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[</span><span class="str">'$null'</span><span class="pun">,</span><span class="pln"> </span><span class="pun">{</span><span class="str">'apiKey'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">10</span><span class="pun">,</span><span class="pln"> </span><span class="str">'eventLog'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">7</span><span class="pun">,</span><span class="pln"> </span><span class="str">'locale'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">12</span><span class="pun">,</span><span class="pln"> </span><span class="str">'$class'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">14</span><span class="pun">,</span><span class="pln"> </span><span class="str">'pauseTime'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">4</span><span class="pun">,</span><span class="pln"> </span><span class="str">'totalErrorCount'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'internetAvailable'</span><span class="pun">:</span><span class="pln"> </span><span class="kwd">True</span><span class="pun">,</span><span class="pln"> </span><span class="str">'errors'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">9</span><span class="pun">,</span><span class="pln"> </span><span class="str">'userID'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'appVersion'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">11</span><span class="pun">,</span><span class="pln"> </span><span class="str">'latitude'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0.0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'eventCounts'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">5</span><span class="pun">,</span><span class="pln"> </span><span class="str">'eventLogComplete'</span><span class="pun">:</span><span class="pln"> </span><span class="kwd">True</span><span class="pun">,</span><span class="pln"> </span><span class="str">'crashed'</span><span class="pun">:</span><span class="pln"> </span><span class="kwd">False</span><span class="pun">,</span><span class="pln"> </span><span class="str">'pageViewCount'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'startTime'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">2</span><span class="pun">,</span><span class="pln"> </span><span class="str">'pauseIntervalMillis'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'gender'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="str">'longitude'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0.0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'serializationVersion'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="str">'timeZone'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">13</span><span class="pun">,</span><span class="pln"> </span><span class="str">'accuracy'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0.0</span><span class="pun">},</span><span class="pln"> </span><span class="pun">{</span><span class="str">'$class'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NS.time'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">378032076.116256</span><span class="pun">},</span><span class="pln"> </span><span class="pun">{</span><span class="str">'$classes'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[</span><span class="str">'NSDate'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NSObject'</span><span class="pun">],</span><span class="pln"> </span><span class="str">'$classname'</span><span class="pun">:</span><span class="pln"> </span><span class="str">'NSDate'</span><span class="pun">},</span><span class="pln"> </span><span class="pun">{</span><span class="str">'$class'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NS.time'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">378032077.674404</span><span class="pun">},</span><span class="pln"> </span><span class="pun">{</span><span class="str">'$class'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">6</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NS.keys'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[],</span><span class="pln"> </span><span class="str">'NS.objects'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[]},</span><span class="pln"> </span><span class="pun">{</span><span class="str">'$classes'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[</span><span class="str">'NSMutableDictionary'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NSDictionary'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NSObject'</span><span class="pun">],</span><span class="pln"> </span><span class="str">'$classname'</span><span class="pun">:</span><span class="pln"> </span><span class="str">'NSMutableDictionary'</span><span class="pun">},</span><span class="pln"> </span><span class="pun">{</span><span class="str">'$class'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">8</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NS.objects'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[]},</span><span class="pln"> </span><span class="pun">{</span><span class="str">'$classes'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[</span><span class="str">'NSMutableArray'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NSArray'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NSObject'</span><span class="pun">],</span><span class="pln"> </span><span class="str">'$classname'</span><span class="pun">:</span><span class="pln"> </span><span class="str">'NSMutableArray'</span><span class="pun">},</span><span class="pln"> </span><span class="pun">{</span><span class="str">'$class'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">8</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NS.objects'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[]},</span><span class="pln"> </span><span class="str">'BMPNB5HT2H63KM42BB83'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'4.0.1'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'en_GB'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'Europe/London'</span><span class="pun">,</span><span class="pln"> </span><span class="pun">{</span><span class="str">'$classes'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[</span><span class="str">'FlurrySession'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NSObject'</span><span class="pun">],</span><span class="pln"> </span><span class="str">'$classname'</span><span class="pun">:</span><span class="pln"> </span><span class="str">'FlurrySession'</span><span class="pun">}],</span><span class="pln"> </span><span class="str">'$top'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">{</span><span class="str">'root'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">1</span><span class="pun">},</span><span class="pln"> </span><span class="str">'$version'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">100000</span><span class="pun">,</span><span class="pln"> </span><span class="str">'$archiver'</span><span class="pun">:</span><span class="pln"> </span><span class="str">'NSKeyedArchiver'</span><span class="pun">}</span></pre><p>The plist is converted to a native Python object (the translations of plist data-type to Python data-types are listed above).  </p><h3><a name="Working_with_NSKeyedArchiver_Files"></a>Working with NSKeyedArchiver Files<a href="#Working_with_NSKeyedArchiver_Files" class="section_anchor"></a></h3><p>In this case the plist is one that has been created by Apple's NSKeyedArchiver class which means it's not a whole lot of fun to work with. Luckily, ccl_bplist can deserialise the object and give you the actual structure of the data. </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj </span><span class="pun">=</span><span class="pln"> ccl_bplist</span><span class="pun">.</span><span class="pln">deserialise_NsKeyedArchiver</span><span class="pun">(</span><span class="pln">plist</span><span class="pun">)</span><span class="pln"><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj<br></span><span class="pun">{</span><span class="str">'apiKey'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">10</span><span class="pun">,</span><span class="pln"> </span><span class="str">'eventLog'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">7</span><span class="pun">,</span><span class="pln"> </span><span class="str">'locale'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">12</span><span class="pun">,</span><span class="pln"> </span><span class="str">'$class'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">14</span><span class="pun">,</span><span class="pln"> </span><span class="str">'eventLogComplete'</span><span class="pun">:</span><span class="pln"> </span><span class="kwd">True</span><span class="pun">,</span><span class="pln"> </span><span class="str">'crashed'</span><span class="pun">:</span><span class="pln"> </span><span class="kwd">False</span><span class="pun">,</span><span class="pln"> </span><span class="str">'pageViewCount'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'startTime'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">2</span><span class="pun">,</span><span class="pln"> </span><span class="str">'pauseTime'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">4</span><span class="pun">,</span><span class="pln"> </span><span class="str">'totalErrorCount'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'internetAvailable'</span><span class="pun">:</span><span class="pln"> </span><span class="kwd">True</span><span class="pun">,</span><span class="pln"> </span><span class="str">'errors'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">9</span><span class="pun">,</span><span class="pln"> </span><span class="str">'pauseIntervalMillis'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'gender'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="str">'userID'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'appVersion'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">11</span><span class="pun">,</span><span class="pln"> </span><span class="str">'longitude'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0.0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'serializationVersion'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="str">'latitude'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0.0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'timeZone'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">13</span><span class="pun">,</span><span class="pln"> </span><span class="str">'accuracy'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0.0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'eventCounts'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">5</span><span class="pun">}</span></pre><p>The module assumes that if the top-level dictionary structure is <tt>$top/root</tt> that the object that you want returning sits beneath <tt>top</tt>. You can override this behaviour is you prefer: </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj </span><span class="pun">=</span><span class="pln"> ccl_bplist</span><span class="pun">.</span><span class="pln">deserialise_NsKeyedArchiver</span><span class="pun">(</span><span class="pln">plist</span><span class="pun">,</span><span class="pln"> parse_whole_structure</span><span class="pun">=</span><span class="kwd">True</span><span class="pun">)</span><span class="pln"><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj<br></span><span class="pun">{</span><span class="str">'root'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">1</span><span class="pun">}</span></pre><p>You'll notice in both of these cases that we have <tt>UID</tt> objects. This is because NSKeyedArchiver maintains an object-table, and in the structure the objects are referred by their position in the object-table (more details here: <a href="http://www.cclgroupltd.com/digital-forensics/rd/geek-post-nskeyedarchiver-files-%E2%80%93-what-are-they-and-how-can-i-use-them.html" rel="nofollow">http://www.cclgroupltd.com/digital-forensics/rd/geek-post-nskeyedarchiver-files-%E2%80%93-what-are-they-and-how-can-i-use-them.html</a>. The module doesn't look-up the objects until they are requested, both for speed and (mostly) because you can have infinitely recursing structures. If you access a UID object in a list or dictionary it will be looked up and returned: </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">]</span><span class="pln"><br></span><span class="pun">{</span><span class="str">'apiKey'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">10</span><span class="pun">,</span><span class="pln"> </span><span class="str">'eventLog'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">7</span><span class="pun">,</span><span class="pln"> </span><span class="str">'locale'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">12</span><span class="pun">,</span><span class="pln"> </span><span class="str">'$class'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">14</span><span class="pun">,</span><span class="pln"> </span><span class="str">'eventLogComplete'</span><span class="pun">:</span><span class="pln"> </span><span class="kwd">True</span><span class="pun">,</span><span class="pln"> </span><span class="str">'crashed'</span><span class="pun">:</span><span class="pln"> </span><span class="kwd">False</span><span class="pun">,</span><span class="pln"> </span><span class="str">'pageViewCount'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'startTime'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">2</span><span class="pun">,</span><span class="pln"> </span><span class="str">'pauseTime'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">4</span><span class="pun">,</span><span class="pln"> </span><span class="str">'totalErrorCount'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'internetAvailable'</span><span class="pun">:</span><span class="pln"> </span><span class="kwd">True</span><span class="pun">,</span><span class="pln"> </span><span class="str">'errors'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">9</span><span class="pun">,</span><span class="pln"> </span><span class="str">'pauseIntervalMillis'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'gender'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="str">'userID'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'appVersion'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">11</span><span class="pun">,</span><span class="pln"> </span><span class="str">'longitude'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0.0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'serializationVersion'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="str">'latitude'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0.0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'timeZone'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">13</span><span class="pun">,</span><span class="pln"> </span><span class="str">'accuracy'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">0.0</span><span class="pun">,</span><span class="pln"> </span><span class="str">'eventCounts'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">5</span><span class="pun">}</span></pre><h3><a name="Automatic_Conversion_of_Common_NSObjects"></a>Automatic Conversion of Common NSObjects<a href="#Automatic_Conversion_of_Common_NSObjects" class="section_anchor"></a></h3><p>NSKeyed Archiver contains serialisations of ObjectiveC objects which would usually require extra code to deal with, but in version 0.13 of the module we've added a set of convenience features to make dealing with these data types a lot simpler. </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">][</span><span class="str">"eventLog"</span><span class="pun">]</span><span class="pln"><br></span><span class="pun">{</span><span class="str">'$class'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">8</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NS.objects'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[]}</span></pre><p>Here we've accessed an object in this plist, we can inspect the type of the object by looking at the "$class" key: </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">][</span><span class="str">"eventLog"</span><span class="pun">][</span><span class="str">"$class"</span><span class="pun">]</span><span class="pln"><br></span><span class="pun">{</span><span class="str">'$classes'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[</span><span class="str">'NSMutableArray'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NSArray'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NSObject'</span><span class="pun">],</span><span class="pln"> </span><span class="str">'$classname'</span><span class="pun">:</span><span class="pln"> </span><span class="str">'NSMutableArray'</span><span class="pun">}</span></pre><p>We can see that this is a serialisation of an <tt>NSMutableArray</tt>. We could access the contents of the array in the <tt>NS.objects</tt> key (which in this case contains an empty list), alternatively we can set a converter function for the module to use, you can write your own, but the module comes with one built in which you can enable like this: </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ccl_bplist</span><span class="pun">.</span><span class="pln">set_object_converter</span><span class="pun">(</span><span class="pln">ccl_bplist</span><span class="pun">.</span><span class="typ">NSKeyedArchiver_common_objects_convertor</span><span class="pun">)</span></pre><p>(NB this enables the converter module-wide, not just for objects that you're currently working on) </p><p>If we access the same object now, it automatically gets converted into a nice, native Python list: </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">][</span><span class="str">"eventLog"</span><span class="pun">]</span><span class="pln"><br></span><span class="pun">[]</span></pre><p>If you want to turn this functionality off, just set the converter function to a pass-through function: </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ccl_bplist</span><span class="pun">.</span><span class="pln">set_object_converter</span><span class="pun">(</span><span class="kwd">lambda</span><span class="pln"> x</span><span class="pun">:</span><span class="pln"> x</span><span class="pun">)</span></pre><p>This built-in converter also works for NSDictionary: </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">][</span><span class="str">"eventCounts"</span><span class="pun">]</span><span class="pln"><br></span><span class="pun">{</span><span class="str">'$class'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">6</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NS.keys'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[],</span><span class="pln"> </span><span class="str">'NS.objects'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[]}</span><span class="pln"><br><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">][</span><span class="str">"eventCounts"</span><span class="pun">][</span><span class="str">"$class"</span><span class="pun">]</span><span class="pln"><br></span><span class="pun">{</span><span class="str">'$classes'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[</span><span class="str">'NSMutableDictionary'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NSDictionary'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NSObject'</span><span class="pun">],</span><span class="pln"> </span><span class="str">'$classname'</span><span class="pun">:</span><span class="pln"> </span><span class="str">'NSMutableDictionary'</span><span class="pun">}</span><span class="pln"><br><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ccl_bplist</span><span class="pun">.</span><span class="pln">set_object_converter</span><span class="pun">(</span><span class="pln">ccl_bplist</span><span class="pun">.</span><span class="typ">NSKeyedArchiver_common_objects_convertor</span><span class="pun">)</span><span class="pln"><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">][</span><span class="str">"eventCounts"</span><span class="pun">]</span><span class="pln"><br></span><span class="pun">{}</span><span class="pln"><br><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ccl_bplist</span><span class="pun">.</span><span class="pln">set_object_converter</span><span class="pun">(</span><span class="kwd">lambda</span><span class="pln"> x</span><span class="pun">:</span><span class="pln"> x</span><span class="pun">)</span></pre><p>NSDate: </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">][</span><span class="str">"startTime"</span><span class="pun">]</span><span class="pln"><br></span><span class="pun">{</span><span class="str">'$class'</span><span class="pun">:</span><span class="pln"> UID</span><span class="pun">:</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NS.time'</span><span class="pun">:</span><span class="pln"> </span><span class="lit">378032076.116256</span><span class="pun">}</span><span class="pln"><br><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">][</span><span class="str">"startTime"</span><span class="pun">][</span><span class="str">"$class"</span><span class="pun">]</span><span class="pln"><br></span><span class="pun">{</span><span class="str">'$classes'</span><span class="pun">:</span><span class="pln"> </span><span class="pun">[</span><span class="str">'NSDate'</span><span class="pun">,</span><span class="pln"> </span><span class="str">'NSObject'</span><span class="pun">],</span><span class="pln"> </span><span class="str">'$classname'</span><span class="pun">:</span><span class="pln"> </span><span class="str">'NSDate'</span><span class="pun">}</span><span class="pln"><br><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ccl_bplist</span><span class="pun">.</span><span class="pln">set_object_converter</span><span class="pun">(</span><span class="pln">ccl_bplist</span><span class="pun">.</span><span class="typ">NSKeyedArchiver_common_objects_convertor</span><span class="pun">)</span><span class="pln"><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">][</span><span class="str">"startTime"</span><span class="pun">]</span><span class="pln"><br>datetime</span><span class="pun">.</span><span class="pln">datetime</span><span class="pun">(</span><span class="lit">2012</span><span class="pun">,</span><span class="pln"> </span><span class="lit">12</span><span class="pun">,</span><span class="pln"> </span><span class="lit">24</span><span class="pun">,</span><span class="pln"> </span><span class="lit">8</span><span class="pun">,</span><span class="pln"> </span><span class="lit">54</span><span class="pun">,</span><span class="pln"> </span><span class="lit">36</span><span class="pun">,</span><span class="pln"> </span><span class="lit">116256</span><span class="pun">)</span><span class="pln"><br><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ccl_bplist</span><span class="pun">.</span><span class="pln">set_object_converter</span><span class="pun">(</span><span class="kwd">lambda</span><span class="pln"> x</span><span class="pun">:</span><span class="pln"> x</span><span class="pun">)</span></pre><p>and the way that NSKeyedArchiver serialises Null as a string containing "$null": </p><pre class="prettyprint"><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">][</span><span class="str">"userID"</span><span class="pun">]</span><span class="pln"><br></span><span class="str">'$null'</span><span class="pln"><br><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> ccl_bplist</span><span class="pun">.</span><span class="pln">set_object_converter</span><span class="pun">(</span><span class="pln">ccl_bplist</span><span class="pun">.</span><span class="typ">NSKeyedArchiver_common_objects_convertor</span><span class="pun">)</span><span class="pln"><br></span><span class="pun">&gt;&gt;&gt;</span><span class="pln"> </span><span class="kwd">print</span><span class="pun">(</span><span class="pln">ns_keyed_archiver_obj</span><span class="pun">[</span><span class="str">"root"</span><span class="pun">][</span><span class="str">"userID"</span><span class="pun">])</span><span class="pln"><br></span><span class="kwd">None</span></pre><hr><h2><a name="Other_projects"></a>Other projects<a href="#Other_projects" class="section_anchor"></a></h2><ul><li> <a href="http://code.google.com/p/ccl-asl/" rel="nofollow">http://code.google.com/p/ccl-asl/</a> - ccl_asl: Python module and command line interface for offline processing of iOS and OSX ASL (Apple System Log) files </li><li> <a href="http://code.google.com/p/ccl-ipd/" rel="nofollow">http://code.google.com/p/ccl-ipd/</a> - ccl_ipd: Python module for parsing BlackBerry IPD backup files </li><li> <a href="http://code.google.com/p/ccl-ssns/" rel="nofollow">http://code.google.com/p/ccl-ssns/</a> - ccl_ssns: Python module and command line interface for parsing Chrome session files (Last Tabs, Current Session, etc.) </li></ul>
 </td>
