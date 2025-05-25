# Lernjournal 3 ONNX

## Übersicht

| | Bitte ausfüllen |
| -------- | ------- |
| ONNX Modell für Analyse (Netron) | URL |
| onnx-image-classification Fork (EfficientNet-Lite) | URL |

## Dokumentation ONNX Analyse

## Layer 1

Im Rahmen dieser Analyse wurde das quantisierte ONNX-Modell EfficientNet-Lite4-11-qdq mit dem Tool Netron geöffnet und im Detail untersucht. Ziel war es, den Aufbau eines ressourcenschonenden Modells zu verstehen, das für den Einsatz auf mobilen oder eingebetteten Systemen optimiert ist. Dazu wurden exemplarisch drei Layer analysiert und ihre Funktion im Kontext des Modells erläutert.

Der erste untersuchte Layer ist Transpose. Dieser Layer bringt die Eingabedaten vom klassischen NHWC-Format (Height × Width × Channels) in das von ONNX bevorzugte NCHW-Format (Channels × Height × Width). Dieser Schritt ist notwendig, da viele Operationen in ONNX – wie z. B. Convolution – dieses Datenformat voraussetzen. Die Tensorform ändert sich dabei von (1 × 224 × 224 × 3) auf (1 × 3 × 224 × 224).

Anschließend wurde der Layer QuantizeLinear betrachtet. Dieser Layer konvertiert Floating-Point-Werte in quantisierte Ganzzahlen, typischerweise INT8, um die Inferenz effizienter zu gestalten. Der Layer verwendet dafür einen Skalierungsfaktor (y_scale) und einen Offset (y_zero_point). In der analysierten Modellversion waren dies beispielhaft y_scale = 0.0078125 und y_zero_point = 127. Diese Transformation spart Speicher und Rechenleistung, was besonders bei mobilen Anwendungen entscheidend ist.

Ein weiterer zentraler Layer im Modell ist DequantizeLinear, der in der analysierten Struktur mehrfach vorkommt – unter anderem im Zusammenhang mit Depthwise-Convolution-Blöcken. Dieser Layer hebt die Quantisierung der Bias-Werte wieder auf, bevor sie in der eigentlichen Convolution verwendet werden. Die ursprünglichen, quantisierten Werte werden mithilfe eines Skalierungsfaktors und eines Offsets in Gleitkommazahlen umgerechnet. Das ist notwendig, da Bias-Werte und Filtergewichte häufig quantisiert gespeichert werden, für Berechnungen aber in höherer Präzision (z. B. FP32) benötigt werden. Insbesondere bei depthwise_conv2d handelt es sich um eine Form der Convolution, bei der jeder Eingangskanal separat verarbeitet wird – eine Technik, die in EfficientNet zur Reduktion des Rechenaufwands verwendet wird.

Durch die Analyse dieser Layer konnte ein gutes Verständnis für die Struktur und die Optimierungen von quantisierten ONNX-Modellen gewonnen werden. Die Visualisierung in Netron hilft dabei, komplexe Abläufe wie das Zusammenspiel von Quantisierung, Dequantisierung und Faltungsschritten nachvollziehbar darzustellen.

## Layer 2

In einem frühen Abschnitt des EfficientNet-Lite4-Modells lässt sich ein typisches Verarbeitungsschema quantisierter Netze erkennen: Zuerst werden die Eingabedaten, Filtergewichte und Bias-Werte mit DequantizeLinear in Gleitkommazahlen konvertiert. Diese Umrechnung ist nötig, da die darauffolgende Faltung (Conv) mit Float-Werten durchgeführt wird. Der Conv-Layer extrahiert dabei mit mehreren Filtern erste Bildmerkmale. Im Anschluss werden die Ergebnisse durch QuantizeLinear erneut in INT8-Werte umgerechnet, um die Effizienz des Modells beizubehalten. Dieses Muster ist typisch für quantisierte Modelle und zeigt, wie ONNX eine Balance zwischen Genauigkeit und Performance ermöglicht.

## vertiefte Struktur

Im Abschnitt blocks_0 beginnt die eigentliche vertiefte Struktur des Modells. Innerhalb dieses Blocks werden mehrere Operationen kombiniert: Zunächst erfolgt eine DequantizeLinear-Operation auf die Eingabedaten und die Gewichte. Danach folgt eine depthwise_conv2d, die pro Kanal eine eigene Faltung durchführt – typisch für MobileNet-ähnliche Architekturen. Das Ergebnis wird durch eine BatchNormalization stabilisiert und anschließend durch QuantizeLinear wieder in INT8 überführt. Solche Blocks wiederholen sich mehrfach im Modell, wobei sich Filteranzahl, Kernelgrößen und Skalierungswerte jeweils ändern.

## Dokumentation onnx-image-classification

* [ ] TODO
