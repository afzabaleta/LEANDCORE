# Hierarchy Diagram

This diagram represents the inheritance and implementation hierarchies
identified in the preliminary analysis of LEANDCORE.

The current hierarchy corresponds to the biometric service, where
`MockBiometricsService` provides an alternative implementation of
`BiometricsService` for testing purposes.

```mermaid
classDiagram

    %% ===== BIOMETRICS SERVICE HIERARCHY =====

    class BiometricsService {
        +authenticate(userId: Long) boolean
    }

    class MockBiometricsService {
        +authenticate(userId: Long) boolean
    }

    BiometricsService <|.. MockBiometricsService
```