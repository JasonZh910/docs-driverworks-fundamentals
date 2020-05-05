## Sample `um_driver.xml`


This `um_driver.xml` code is be best viewed and modified in a text editor by opening the file from the DriverWorks SDK. The file can be located at: DriverWorks SDK\Samples\Universal Minidrivers

In general, you should merge the XML in the example with the existing XML of your driver. Pay attention to additionally commented sections for special instructions.

### Usage Note: 

The AV switcher proxy ID is 5999 in this XML. This is probably not acceptable for your project; make the proxy ID sequential with your other proxies.

	devicedata>
	 <copyright>Copyright 2019 Control4 Corporation. All rights reserved.</copyright>
	 <config>
	  <properties>
	   <property>
	    <name>Passthrough Mode</name>
	    <type>LIST</type>
	    <items>
	     <item>Off</item>
	     <item>On</item>
	    </items>
	    <default>On</default>
	    <readonly>false</readonly>
	    <tooltip>If set to 'On', mini-apps will stay selected and pass-through commands.  If 'Off', this driver will be reselected.</tooltip>
	   </property>
	  </properties>
	 </config>
	 <proxies>
	  <!--
	  If your main proxy is a TV, receiver, AV switch or other proxy that receives SET_INPUT commands when selecting the AV path,you don't need to include this additional proxy.
	  Alternatively, if you already have an AV switch proxy as part of your driver, you may be able to incorporate the RF_MINI_APP connections into that proxy.
	  If you need to include this proxy, make the binding ID one more than the last other proxy of your driver.  It's numbered 5999 here for demonstration.
	  -->
	  <proxy proxybindingid="5999" name="App Switcher">avswitch</proxy>
	 </proxies>
	 <connections>
	  <!--
	  Connection for AVswitch proxy as defined in proxies section above.
	  Only include this connection if you also needed to include the extra avswitch proxy above
	  -->
	  <connection>
	   <id>5999</id>
	   <type>2</type>
	   <connectionname>AVSWITCH</connectionname>
	   <consumer>False</consumer>
	   <linelevel>True</linelevel>
	   <classes>
	    <class>
	     <classname>AVSWITCH</classname>
	    </class>
	   </classes>
	  </connection>
	  <!-- Video connection out of switcher - connect this (with autobind or C4:Bind) to your "main" proxy.  COMPONENT class not be needed if your proxy only does HDMI
	  Only include this connection if you also needed to include the extra avswitch proxy above
	  -->
	  <connection proxybindingid="5999">
	   <id>2110</id>
	   <type>5</type>
	   <connectionname>App Switch Video Out</connectionname>
	   <consumer>False</consumer>
	   <linelevel>True</linelevel>
	   <hidden>True</hidden>
	   <classes>
	    <class>
	     <classname>COMPONENT</classname>
	     <autobind>true</autobind>
	    </class>
	    <class>
	     <classname>HDMI</classname>
	     <autobind>true</autobind>
	    </class>
	   </classes>
	  </connection>
	  <!-- Audio connection out of switcher - connect this (with autobind or C4:Bind) to your "main" proxy.  May not be needed if       your proxy only does HDMI
	  Only include this connection if you also needed to include the extra avswitch proxy above
	  -->
	  <connection proxybindingid="5999">
	   <id>4110</id>
	   <type>6</type>
	   <connectionname>App Switch Audio Out</connectionname>
	   <consumer>False</consumer>
	   <linelevel>True</linelevel>
	   <hidden>True</hidden>
	   <classes>
	    <class>
	     <classname>STEREO</classname>
	     <autobind>true</autobind>
	    </class>
	    <class>
	     <classname>DIGITAL_COAX</classname>
	     <autobind>true</autobind>
	    </class>
	    <class>
	     <classname>DIGITAL_OPTICAL</classname>
	     <autobind>true</autobind>
	    </class>
	   </classes>
	  </connection>
	  <!-- RF Connections for universal minidrivers.  These are in the range 3101-3125; more can be added if necessary.  Reflect        this in the driver.lua code -->
	  <!-- Note that for  Receiver/TV proxies, inputs over x099 will not trigger events, variable changes or conditionals.-->
	  <connection proxybindingid="5999">
	   <id>3101</id>
	   <type>5</type>
	   <connectionname>MiniApp 1</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3102</id>
	   <type>5</type>
	   <connectionname>MiniApp 2</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3103</id>
	   <type>5</type>
	   <connectionname>MiniApp 3</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3104</id>
	   <type>5</type>
	   <connectionname>MiniApp 4</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3105</id>
	   <type>5</type>
	   <connectionname>MiniApp 5</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3106</id>
	   <type>5</type>
	   <connectionname>MiniApp 6</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3107</id>
	   <type>5</type>
	   <connectionname>MiniApp 7</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3108</id>
	   <type>5</type>
	   <connectionname>MiniApp 8</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3109</id>
	   <type>5</type>
	   <connectionname>MiniApp 9</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3110</id>
	   <type>5</type>
	   <connectionname>MiniApp 10</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3111</id>
	   <type>5</type>
	   <connectionname>MiniApp 11</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3112</id>
	   <type>5</type>
	   <connectionname>MiniApp 12</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3113</id>
	   <type>5</type>
	   <connectionname>MiniApp 13</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3114</id>
	   <type>5</type>
	   <connectionname>MiniApp 14</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3115</id>
	   <type>5</type>
	   <connectionname>MiniApp 15</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3116</id>
	   <type>5</type>
	   <connectionname>MiniApp 16</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3117</id>
	   <type>5</type>
	   <connectionname>MiniApp 17</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3118</id>
	   <type>5</type>
	   <connectionname>MiniApp 18</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3119</id>
	   <type>5</type>
	   <connectionname>MiniApp 19</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3120</id>
	   <type>5</type>
	   <connectionname>MiniApp 20</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3121</id>
	   <type>5</type>
	   <connectionname>MiniApp 21</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3122</id>
	   <type>5</type>
	   <connectionname>MiniApp 22</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3123</id>
	   <type>5</type>
	   <connectionname>MiniApp 23</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3124</id>
	   <type>5</type>
	   <connectionname>MiniApp 24</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	  <connection proxybindingid="5999">
	   <id>3125</id>
	   <type>5</type>
	   <connectionname>MiniApp 25</connectionname>
	   <consumer>True</consumer>
	   <linelevel>False</linelevel>
	   <classes>
	    <class>
	     <classname>RF_MINI_APP</classname>
	    </class>
	   </classes>
	  </connection>
	 </connections>
	</devicedata>
