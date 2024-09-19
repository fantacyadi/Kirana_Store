@Autowired
private RateLimiterService rateLimiterService;

@PostMapping("/add")
public ResponseEntity<?> addTransaction(@RequestBody Transaction transaction) {
    if (!rateLimiterService.allowRequest()) {
        return ResponseEntity.status(HttpStatus.TOO_MANY_REQUESTS).build();
    }
    return ResponseEntity.ok(transactionService.saveTransaction(transaction));
}
