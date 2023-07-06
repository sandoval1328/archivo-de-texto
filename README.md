#include <iostream>
#include <vector>
#include <cmath>
#include <limits>

struct Punto {
    int x;
    int y;
};

double calcularDistancia(const Punto& punto1, const Punto& punto2) {
    int dx = punto1.x - punto2.x;
    int dy = punto1.y - punto2.y;
    return std::sqrt(dx*dx + dy*dy);
}

void encontrarPuntosMasCercanos(const std::vector<Punto>& puntos) {
    double distanciaMinima = std::numeric_limits<double>::max();
    Punto punto1, punto2;

    for (size_t i = 0; i < puntos.size(); i++) {
        for (size_t j = i + 1; j < puntos.size(); j++) {
            double distancia = calcularDistancia(puntos[i], puntos[j]);
            if (distancia < distanciaMinima) {
                distanciaMinima = distancia;
                punto1 = puntos[i];
                punto2 = puntos[j];
            }
        }
    }

    std::cout << "Los puntos mas cercanos son (" << punto1.x << ", " << punto1.y << ") y (" << punto2.x << ", " << punto2.y << ") con una distancia de " << distanciaMinima << " unidades." << std::endl;
}

int main() {
    int n;
    std::cout << "Ingrese la cantidad de puntos: ";
    std::cin >> n;

    std::vector<Punto> puntos(n);
    std::cout << "Ingrese las coordenadas de los puntos separadas por espacios (x y): ";
    for (int i = 0; i < n; i++) {
        std::cin >> puntos[i].x >> puntos[i].y;
    }

    encontrarPuntosMasCercanos(puntos);

    return 0;
}
