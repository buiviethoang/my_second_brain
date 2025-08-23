2025-08-23 15:00
Status: #baby
Tags: [[design pattern]]
## Main

The **Adapter Pattern** allows **two incompatible interfaces to work together**.

- It acts as a **wrapper** around an existing object.
    
- The client can call the adapter instead of directly using the incompatible interface.
    

👉 Think of it as a **power plug adapter**:

- Your device has a US plug.
    
- The wall socket is EU style.
    
- The adapter allows the US plug to fit into the EU socket.

```java
// Target interface
interface MediaPlayer {
    void play(String audioType, String fileName);
}

// Adaptee
class AdvancedMediaPlayer {
    public void playVlc(String fileName) {
        System.out.println("Playing vlc file: " + fileName);
    }

    public void playMp4(String fileName) {
        System.out.println("Playing mp4 file: " + fileName);
    }
}

// Adapter
class MediaAdapter implements MediaPlayer {
    AdvancedMediaPlayer advancedMusicPlayer;

    public MediaAdapter(String audioType) {
        advancedMusicPlayer = new AdvancedMediaPlayer();
    }

    @Override
    public void play(String audioType, String fileName) {
        if(audioType.equalsIgnoreCase("vlc")) {
            advancedMusicPlayer.playVlc(fileName);
        } else if(audioType.equalsIgnoreCase("mp4")) {
            advancedMusicPlayer.playMp4(fileName);
        }
    }
}

// Client
class AudioPlayer implements MediaPlayer {
    MediaAdapter mediaAdapter;

    @Override
    public void play(String audioType, String fileName) {
        if(audioType.equalsIgnoreCase("mp3")) {
            System.out.println("Playing mp3 file: " + fileName);
        } 
        else if(audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")) {
            mediaAdapter = new MediaAdapter(audioType);
            mediaAdapter.play(audioType, fileName);
        } 
        else {
            System.out.println("Invalid media. " + audioType + " format not supported");
        }
    }
}

// Demo
public class AdapterPatternDemo {
    public static void main(String[] args) {
        AudioPlayer audioPlayer = new AudioPlayer();

        audioPlayer.play("mp3", "song1.mp3");
        audioPlayer.play("mp4", "song2.mp4");
        audioPlayer.play("vlc", "song3.vlc");
        audioPlayer.play("avi", "song4.avi");
    }
}

```

### 🔹 **When to Use**

- You want to **reuse an existing class** but its interface doesn’t match what the client expects.
    
- You want to **decouple client code from implementation classes**.
    
- You need to **integrate third-party or legacy code** without changing it.

### 🔹 **Pros**

- Promotes **reuse of existing classes**.
    
- Decouples client from concrete implementations.
    
- Simple to implement.
    

### 🔹 **Cons**

- Can lead to **many small adapter classes**.
    
- Adds another level of indirection.


### Real-wolrd example
```java
interface PaymentProcessor {
    void pay(double amount);
}
class PayPalProcessor implements PaymentProcessor {
    public void pay(double amount) {
        System.out.println("Paid " + amount + " using PayPal");
    }
}


class StripePayment {
    public void makePayment(int cents) {
        System.out.println("Paid " + (cents / 100.0) + " using Stripe");
    }
}

class StripeAdapter implements PaymentProcessor {
    private StripePayment stripe;

    public StripeAdapter(StripePayment stripe) {
        this.stripe = stripe;
    }

    @Override
    public void pay(double amount) {
        int cents = (int) (amount * 100);
        stripe.makePayment(cents);
    }
}


public class ECommerceApp {
    public static void main(String[] args) {
        PaymentProcessor paypal = new PayPalProcessor();
        paypal.pay(50.0);

        StripePayment stripe = new StripePayment();
        PaymentProcessor stripeAdapter = new StripeAdapter(stripe);
        stripeAdapter.pay(75.0);
    }
}



```

### **Why Adapter is Useful Here**

- The e-commerce system **doesn’t need to change** to support Stripe.
    
- Stripe’s **incompatible interface** is adapted to the expected `PaymentProcessor` interface.
    
- Makes the system **extensible** for future payment gateways (just create another adapter).
## References