import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.module.SimpleModule;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class JacksonConfig {

    @Bean
    public ObjectMapper objectMapper() {
        ObjectMapper objectMapper = new ObjectMapper();

        // Option 1: Trust specific class
        SimpleModule module = new SimpleModule();
        module.addDeserializer(bac.deposit.cash.rules.batch.ReconTxn.class, new ReconTxnDeserializer());
        objectMapper.registerModule(module);

        // Option 2: Enable default typing (caution: more permissive)
        objectMapper.activateDefaultTyping(LaissezFaireSubTypeValidator.instance, ObjectMapper.DefaultTyping.NON_FINAL);

        return objectMapper;
    }
}
