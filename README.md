# OBD Metrics Test
[![Deploy](https://github.com/tzebrowski/ObdMetricsTest/actions/workflows/deploy.yml/badge.svg)](https://github.com/tzebrowski/ObdMetricsTest/actions/workflows/deploy.yml)

## About

This project contains set of utilities which allows to tests OBD2 PIDs with the focus on business aspects of its development.


## Usage

The framework under `org.obd.metrics.test` package exposes set of interfaces like: `CodecTest` which allows to write clean PIDs tests .

```java

interface MultiJet_2_2_Test extends CodecTest {

	final String RESOURCE_NAME = "giulia_2_2_multijet.json";

	@Override
	default String getPidFile() {
		return RESOURCE_NAME;
	}
}

public class AirTempMafTest implements MultiJet_2_2_Test {

	@ParameterizedTest
	@CsvSource(value = { 
			"62193F0000=-40",
			"62193F1100=47",
	}, delimiter = '=')
	public void test(String input, Integer expected) {
		assertEquals(input, expected);
	}
}
```

